---
layout: post
title: GitLab的Webhooks自动化部署
category: gitlab
comments: true
tags:
- gitlab
---

# [使用 GitHub / GitLab 的 Webhooks 进行网站自动化部署](http://www.lovelucy.info/auto-deploy-website-by-webhooks-of-github-and-gitlab.html)

```
老早就想写这个话题了，今天正好有机会研究了一下 git 的自动化部署。最终做到的效果就是，每当有新的 commit push 到 master 分支的时候，就自动在测试/生产服务器上进行 git pull 拉取最新的代码，免去了程序猿兼职运维 ssh 上去拉代码部署的重复性工作。我们也要 Agile development 不是？什么敏捷开发啊，极限编程啊，快速迭代啊，持续集成啊，精益创业啊，口号怎么高端怎么来，最后就是写了个自动化脚本……
```

## 一、自动化部署脚本

首先要保证要部署的 Web 目录就是 git clone 下来的一个 repository。这样 rollback 也方便，直接 checkout 某一个历史版本就好。

很简单地写了个 shell 脚本 deploy.sh
```
#!/bin/bash
 
WEB_PATH='/var/www/dev.lovelucy.info'
WEB_USER='lovelucydev'
WEB_USERGROUP='lovelucydev'
 
echo "Start deployment"
cd $WEB_PATH
echo "pulling source code..."
git reset --hard origin/master
git clean -f
git pull
git checkout master
echo "changing permissions..."
chown -R $WEB_USER:$WEB_USERGROUP $WEB_PATH
echo "Finished."
```

下面要做的就是每当有 push 的时候就自动调用这个脚本。

***

## 二、监听 Web Hooks
GitHub 和 GitLab 本身都支持 Webhooks 的设定
![](http://www.lovelucy.info/wordpress/wp-content/uploads/2015/01/github-webhooks-900x589.jpg)
![](http://www.lovelucy.info/wordpress/wp-content/uploads/2015/01/gitlab-webhooks-900x347.jpg)

那个 Payload URL 上填上需要部署到的服务器的网址，比方说 http://dev.lovelucy.info/incoming。然后之后每次有 push 事件 GitHub 都会主动往这个地址发送一个 POST 请求，当然你也可以选择任何事件都发个 POST 通知你。GitHub 还有个 Secret 的设定，就是一个字符串，如果加上的话就在 POST 请求的 HTTP 头中会带一个 Hash 值做验证密文，证明这个 POST 真是来自 GitHub，不然任何人都往那个地址 POST 忽悠你你都不知道谁是谁对吧……

然后我们就要写一个脚本在 http://dev.lovelucy.info/incoming 这里接受 POST 请求了。因为本人机器上跑的是 node，俺就找了个 nodejs 的中间件 [github-webhook-handler](https://github.com/rvagg/github-webhook-handler) 。如果你要部署的是 PHP 网站，那你应该找一个世界上最好的语言 PHP 的版本，或者自己写一个，只需要接收 $_POST 嘛，好简单的，不多废话啦。么么哒 ( • ̀ω•́ )
```
$ npm install -g github-webhook-handler
```
鉴于在天朝的服务器上 npm 拉 repo 比拉屎还难的状况，我们可以 选用 阿里的镜像，据说 10 分钟和官方同步一次。_(:3 」∠ )_
```
$ npm install -g cnpm --registry=http://r.cnpmjs.org
$ cnpm install -g github-webhook-handler
```
好了，万事俱备，下面是 NodeJS 的监听程序 deploy.js
```
var http = require('http')
var createHandler = require('github-webhook-handler')
var handler = createHandler({ path: '/incoming', secret: 'myHashSecret' }) 
// 上面的 secret 保持和 GitHub 后台设置的一致
 
function run_cmd(cmd, args, callback) {
  var spawn = require('child_process').spawn;
  var child = spawn(cmd, args);
  var resp = "";
 
  child.stdout.on('data', function(buffer) { resp += buffer.toString(); });
  child.stdout.on('end', function() { callback (resp) });
}
 
http.createServer(function (req, res) {
  handler(req, res, function (err) {
    res.statusCode = 404
    res.end('no such location')
  })
}).listen(7777)
 
handler.on('error', function (err) {
  console.error('Error:', err.message)
})
 
handler.on('push', function (event) {
  console.log('Received a push event for %s to %s',
    event.payload.repository.name,
    event.payload.ref);
  run_cmd('sh', ['./deploy-dev.sh'], function(text){ console.log(text) });
})
 
/*
handler.on('issues', function (event) {
  console.log('Received an issue event for % action=%s: #%d %s',
    event.payload.repository.name,
    event.payload.action,
    event.payload.issue.number,
    event.payload.issue.title)
})
*/
```
于是直接就可以跑起来了
```
$ nodejs deploy.js
```
当然为了防止 NodeJS 自己挂掉，我们可以启用进程管理服务 [forever](https://github.com/foreverjs/forever)，它类似 python 里面的 supervisor。
```
$ cnpm install -g forever
$ forever start deploy.js
```
这样就算这段 NodeJS 代码某处出错挂了，它也会自动重新启动一个进程，保证服务仍可用。forever 的几个命令还是蛮简单的
```
$ forever list
$ forever stop 1
$ forever restartall
```
上面的 NodeJS 将 Web 服务跑在了 7777 端口，我们可以用 Nginx 反向代理到 80 端口（可选）
```
server {
    listen 80;
    server_name dev.lovelucy.info;

    # ...

    location / {
        # ...
    }

    location /incoming$ {
        proxy_pass http://127.0.0.1:7777;
    }
}
```

***

## 三、集成第三方 Service
注意到 GitHub 项目后台还有个 Service 的 tab 没？
![](http://www.lovelucy.info/wordpress/wp-content/uploads/2015/01/github-service.jpg)
这是 GitHub 官方集成的大量的第三方服务，有点类似 IFTTT 的节奏，能做的事情就很多了。比如我设定了如果有人 push 代码，就在我们 hipchat 内部聊天群里发一个通知；如果有人提 issue，就自动给他回一封 welcome 的邮件……