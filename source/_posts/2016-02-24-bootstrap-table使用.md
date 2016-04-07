---
layout: post
title: bootstrap-table使用  
category: bootstrap
comments: true
---

# [bootstrap-table使用](http://blog.163.com/wp_2002wp/blog/static/31472252201511142205327/)

```
<table id="table"
   data-toggle="table"
   data-striped ="true"  --条纹
   data-pagination ="true" --分页
   data-side-pagination = "server" --服务器端分页 ('client' 客户端)
   data-show-header ="true" --显示表头
   data-show-footer = "false" --显示表尾部
   data-search = "false" --工具栏 查询框
   data-strict-search = "false" --精确查询
   data-search-text = "" --查询框初始值
   data-search-time-out = "500" --查询timeout时间
   data-trim-on-search = "true" --去掉查询参数空格
   data-show-columns ="true" --工具栏 显示表头信息 可以调整显示行
   data-minimum-count-columns = "1" -- data-show-columns 选项最小显示1列
   data-show-refresh = "true" --工具栏 显示刷新按钮
   data-show-toggle ="true" --工具栏  转换表格为列表显示
   data-card-view = "false" --显示为列表
   data-smart-display ="false" --显示分页或列表
   data-query-params-type = ""
   data-query-params = "queryParams"
   data-page-size = "10"
   data-page-number = "1"
   data-page-list = "[10, 25, 50, 100, 200]"
   data-response-handler = "responseHandler"
   data-url="${syspath}/sys/q/list">
</table>
function responseHandler(res) {
    if(res.total > 0) {
	 return {
	    "rows": res.rows,
	    "total": res.total
	 }
    } else {
	 return {
	    "rows": [],
	    "total": 0
	 }
    }
}
function queryParams(params) {
    return {
       pageSize: params.pageSize,
       pageNumber: params.pageNumber,
       xx: 自定义控件.val()
    };
}
```
