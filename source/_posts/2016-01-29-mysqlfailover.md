---
layout: post
title: mysqlfailover+vip高可用设想
category: mysql
comments: true
tags:
- dba
---

#### [MySQL Auto-Failover 功能测试](http://www.ttlsa.com/mysql/the-mysql-auto-failover-function-test/)
#### MySQL Utilities 1.6 Manual [下载](http://dev.mysql.com/downloads/utilities/1.6.html)
#### [mysqlfailover](https://dev.mysql.com/doc/mysql-utilities/1.5/en/mysqlfailover.html) Automatic replication health monitoring and failover 

```
This utility permits users to perform replication health monitoring and automatic failover on a replication topology consisting of a master and its slaves. The utility is designed to run interactively or continuously refreshing the health information at periodic intervals. Its primary mission is to monitor the master for failure and when a failure occurs, execute failover to the best slave available. The utility accepts a list of slaves to be considered the candidate slave.

This utility is designed to work exclusively for servers that support global transaction identifiers (GTIDs) and have gtid_mode=ON. MySQL server versions 5.6.5 and higher support GTIDs. See Replication with Global Transaction Identifiers for more information.

The user can specify the interval in seconds to use for detecting the master status and generating the health report using the --interval option. At each interval, the utility will check to see if the server is alive via a ping operation followed by a check of the connector to detect if the server is still reachable. The ping operation can be controlled with the --ping option (see below).

If the master is found to be offline or unreachable, the utility will execute one of the following actions based on the --failover-mode option value. The available values are:

auto (default): Execute automatic failover to the list of candidates first and if no slaves are viable, continue to locate a viable candidate from the list of slaves. If no slaves are found to be a viable candidate, the utility will generate and error and exit.

Once a candidate is found, the utility will conduct failover to the best slave. The command will test each candidate slave listed for the prerequisites. Once a candidate slave is elected, it is made a slave of each of the other slaves thereby collecting any transactions executed on other slaves but not the candidate. In this way, the candidate becomes the most up-to-date slave.

elect: This mode is the same as auto, except if no candidates specified in the list of candidate slaves are viable, then it does not check the remaining slaves, and instead generates an error and then exits.

fail: This mode produces an error and does not failover when the master is downed. This mode is used to provide periodic health monitoring without the failover action taken.
```

For all options that permit specifying multiple servers, the options require a comma-separated list of connection parameters in the following form (where the password, port, and socket are optional).:

```
<*user*>[:<*passwd*>]@<*host*>[:<*port*>][:<*socket*>] or <*login-path*>[:<*port*>][:<*socket*>]
```
---

# 安装mysqlfailover

1. 下载MySQL Utilities 1.6 Manual [下载](http://dev.mysql.com/downloads/utilities/1.6.html)
2. 选择[Debian Linux 8.2 (Architecture Independent), DEB](http://cdn.mysql.com//Downloads/Connector-Python/mysql-connector-python_2.1.3-1debian8.2_all.deb)
3. 安装 dpkg -i mysql-connector-python_2.1.3-1debian8.2_all.deb 
4. 创建用户并给予权限： **grant SUPER, GRANT OPTION, REPLICATION SLAVE, SELECT, RELOAD, DROP, CREATE, INSERT on *.* to root@'localhost' identified by 'system';**
5. 运行 mysqlfailover --master=root:system@localhost:3306 --discover-slaves-login=<font color=#8B0000>**root:pass**</font> --log=/tmp/log.txt --force --verbose --daemon=start
6. failover Percona 搭建[参考](https://www.percona.com/blog/2014/07/03/failover-mysql-utilities-part-2-mysqlfailover/) 

# 搭建主从注意事项:

```
搭建主从主机名全部用主机名，即dns域名，如果端口不一致则使用master_port=6666 mysqlfailover会自动发现从的端口(不一样也可以)

mysql> change master to master_host='**com.cstonline.oper.default.data.MHA-01**',<font color=#8B0000>**master_port=6666**</font>,master_user='**root**',master_password='**pass**',master_auto_position=1;
```


---

# 遇到问题以及解决办法

> 报错: [ImportError: No module named connector.conversion](http://stackoverflow.com/questions/24267017/importerror-no-module-named-connector-conversion)

```
From Can't run MySql Utilities:

MYSQL Utilities assumes that the MySQL Connector for Python has been installed. If you install it (http://dev.mysql.com/downloads/connector/python/), MySQL Utilities should run OK.
```

> 报错: Discovering slaves for master at localhost:6666

```
WARNING: There are slaves that have not been registered with --report-host or --report-port (--verbose for more details).
```

> 报错 ERROR: User root on 172.16.1.89@3307 does not have sufficient privileges to execute the failover command (required: SUPER, GRANT OPTION, REPLICATION SLAVE, SELECT, RELOAD, DROP, CREATE, INSERT).

```
grant SUPER, GRANT OPTION, REPLICATION SLAVE, SELECT, RELOAD, DROP, CREATE, INSERT on *.* to root@'localhost' identified by 'system';
```

> 报错 ERROR Failover requires --master-info-repository=TABLE for all slaves.

```
在从端添加参数master_info_repository=TABLE #将master.info文件用table来存储，件事刷新这个文件的频率，5.7也建议，默认FILE
The utility will check to see if the slaves are using the option --master-info-repository=TABLE. If they are not, the utility will stop with an error.
```

> 报错 [ERROR: Query failed. 1406 (22001): Data too long for column 'host' at row 1](http://blog.chinaunix.net/uid-26435987-id-3178010.html)

```
解决办法：
CREATE TABLE `student` (
  `sno`    int(11)     NOT NULL,
  `sname`  varchar(20) NOT NULL,
  `***`    varchar(20) NOT NULL
)DEFAULT CHARSET=utf8;
<上面`***`是性别的英文，被网站系统屏蔽掉了>T_T
就是在上面这个语句后加入DEFAULT CHARSET=utf8即可。
```

# 机制

```
1. 自动检测 
 
2016-01-29 18:59:18 PM INFO Master may be down. Waiting for 3 seconds.

```

# 切换日志 

```
2016-01-29 19:57:41 PM INFO Failed to reconnect to the master after 3 attemps.
2016-01-29 19:57:41 PM CRITICAL Master is confirmed to be down or unreachable.
2016-01-29 19:57:41 PM INFO Failover starting in 'auto' mode...
2016-01-29 19:57:41 PM INFO Checking eligibility of slave debian:3306 for candidate.
2016-01-29 19:57:41 PM INFO GTID_MODE=ON ... Ok
2016-01-29 19:57:41 PM INFO Replication user exists ... Ok
2016-01-29 19:57:41 PM INFO Candidate slave debian:3306 will become the new master.
2016-01-29 19:57:41 PM INFO Checking slaves status (before failover).
2016-01-29 19:57:41 PM INFO Preparing candidate for failover.
2016-01-29 19:57:41 PM INFO No missing transactions found on com.cstonline.oper.default.data.MHA-02:3306. Skipping connection of candidate as slave.
2016-01-29 19:57:41 PM INFO Creating replication user if it does not exist.
2016-01-29 19:57:41 PM INFO Stopping slaves.
2016-01-29 19:57:41 PM INFO Performing STOP on all slaves.
2016-01-29 19:57:41 PM WARNING Executing stop on slave debian:3306 WARN - slave is not configured with this master
2016-01-29 19:57:41 PM INFO Executing stop on slave debian:3306 Ok
2016-01-29 19:57:41 PM WARNING Executing stop on slave com.cstonline.oper.default.data.MHA-02:3306 WARN - slave is not configured with this master
2016-01-29 19:57:41 PM INFO Executing stop on slave com.cstonline.oper.default.data.MHA-02:3306 Ok
2016-01-29 19:57:41 PM INFO Switching slaves to new master.
2016-01-29 19:57:41 PM INFO Disconnecting new master as slave.
2016-01-29 19:57:41 PM INFO Execute on debian:3306: RESET SLAVE ALL
2016-01-29 19:57:41 PM INFO Starting slaves.
2016-01-29 19:57:41 PM INFO Performing START on all slaves.
2016-01-29 19:57:41 PM INFO Executing start on slave com.cstonline.oper.default.data.MHA-02:3306 Ok
2016-01-29 19:57:41 PM INFO Checking slaves for errors.
2016-01-29 19:57:41 PM INFO com.cstonline.oper.default.data.MHA-02:3306 status: Ok
2016-01-29 19:57:41 PM INFO Failover complete.
2016-01-29 19:57:41 PM INFO Discovering slaves for master at debian:3306
2016-01-29 19:57:41 PM INFO Discovering slave at com.cstonline.oper.default.data.MHA-02:3306
2016-01-29 19:57:41 PM INFO Found slave: com.cstonline.oper.default.data.MHA-02:3306
2016-01-29 19:57:41 PM INFO Server 'com.cstonline.oper.default.data.MHA-02:3306' is using MySQL version 5.6.12-log.
2016-01-29 19:57:46 PM INFO Unregistering existing instances from slaves.
2016-01-29 19:57:46 PM INFO Registering instance on master.
2016-01-29 19:57:46 PM INFO Getting health for master: debian:3306.
2016-01-29 19:57:47 PM INFO Master status: binlog: binlog.000004, position:1292
2016-01-29 19:57:47 PM INFO Getting health for master: debian:3306.
2016-01-29 19:57:57 PM INFO Getting health for master: debian:3306.
2016-01-29 19:57:57 PM INFO Master status: binlog: binlog.000004, position:1292
2016-01-29 19:57:57 PM INFO Master status: binlog: binlog.000004, position:1292
```


---
# OPTIONS

```
mysqlfailover accepts the following command-line options:

 --help

Display a help message and exit.

 --license

Display license information and exit.

 --candidates=<candidate slave connections>

Connection information for candidate slave servers. Valid only with failover command. List multiple slaves in comma-separated list.

To connect to a server, it is necessary to specify connection parameters such as user name, host name, password, and either a port or socket. MySQL Utilities provides a number of ways to supply this information. All of the methods require specifying your choice via a command-line option such as --server, --master, --slave, etc. The methods include the following in order of most secure to least secure.

Use login-paths from your .mylogin.cnf file (encrypted, not visible). Example : <login-path>[:<port>][:<socket>]

Use a configuration file (unencrypted, not visible) Note: available in release-1.5.0. Example : <configuration-file-path>[:<section>]

Specify the data on the command-line (unencrypted, visible). Example : <user>[:<passwd>]@<host>[:<port>][:<socket>]

 --daemon=<command>

Run as a daemon. The command can be start (start daemon), stop (stop daemon), restart (stop then start the daemon) or nodetach (start but do not detach the process). This option is only available for POSIX systems.

 --discover-slaves-login=<user:password>

At startup, query master for all registered slaves and use the user name and password specified to connect. Supply the user and password in the form <user>[:<passwd>] or <login-path>. For example, --discover=joe:secret will use 'joe' as the user and 'secret' as the password for each discovered slave.

 --exec-after=<script>

Name of script to execute after failover or switchover. Script name may include the path.

 --exec-before=<script>

Name of script to execute before failover or switchover. Script name may include the path.

 --exec-fail-check=<script>

Name of script to execute on each interval to invoke failover.

 --exec-post-failover=<script>

Name of script to execute after failover is complete and the utility has refreshed the health report.

 --failover-mode=<mode>, -f <mode>

Action to take when the master fails. 'auto' = automatically fail to best slave, 'elect' = fail to candidate list or if no candidate meets criteria fail, 'fail' = take no action and stop when master fails. Default = 'auto'.

 --force

Override the registration check on master for multiple instances of the console monitoring the same master. See notes.

 --interval=<seconds>, -i <seconds>

Interval in seconds for polling the master for failure and reporting health. Default = 15 seconds. Minimum is 5 seconds.

 --log=<log_file>

Specify a log file to use for logging messages

 --log-age=<days>

Specify maximum age of log entries in days. Entries older than this will be purged on startup. Default = 7 days.

 --master=<connection>

Connection information for the master server.

To connect to a server, it is necessary to specify connection parameters such as user name, host name, password, and either a port or socket. MySQL Utilities provides a number of ways to supply this information. All of the methods require specifying your choice via a command-line option such as --server, --master, --slave, etc. The methods include the following in order of most secure to least secure.

Use login-paths from your .mylogin.cnf file (encrypted, not visible). Example : <login-path>[:<port>][:<socket>]

Use a configuration file (unencrypted, not visible) Note: available in release-1.5.0. Example : <configuration-file-path>[:<section>]

Specify the data on the command-line (unencrypted, visible). Example : <user>[:<passwd>]@<host>[:<port>][:<socket>]

 --max-position=<position>

Used to detect slave delay. The maximum difference between the master's log position and the slave's reported read position of the master. A value greater than this means the slave is too far behind the master. Default = 0.

 --pedantic, -p

Used to stop failover if some inconsistencies are found, such as errant transactions on slaves or SQL thread errors, during server checks. By default, the utility only generates warnings if issues are found when checking a slave's status during failover, and it will continue its execution unless this option is specified.

 --pidfile=<pidfile>

Pidfile for running mysqlfailover as a daemon. This file contains the PID (process identifier), that uniquely identifies a process. It is needed to identify and control the process forked by mysqlfailover.

 --ping=<number>

Number of ping attempts for detecting a downed server. Default is 3 seconds.

Note
On some platforms, this is the same as number of seconds to wait for ping to return.

 --report-values=<report_values>

Report values used in mysqlfailover running as a daemon. It can be health, gtid or uuid. Multiple values can be used separated by commas.

health

Display the replication health of the topology.

gtid

Display the master's list of executed GTIDs, contents of the GTID variables; @@GLOBAL.GTID_EXECUTED, @@GLOBAL.GTID_PURGED and @@GLOBAL.GTID_OWNED.

uuid

Display universally unique identifiers (UUIDs) for all servers.

Default = health.

 --rpl-user=:<replication_user>

The user and password for the replication user requirement, in the form: <user>[:<password>] or <login-path>. E.g. rpl:passwd

Default = None.

 --script-threshold=<return_code>

Value for external scripts to trigger aborting the operation if result is greater than or equal to the threshold.

Default = None (no threshold checking).

 --seconds-behind=<seconds>

Used to detect slave delay (only for health reporting purposes). The maximum number of seconds behind the master permitted before slave is considered behind the master in the health report state. Default = 0.

 --slaves=<slave connections>

Connection information for slave servers. List multiple slaves in comma-separated list. The list will be evaluated literally whereby each server is considered a slave to the master listed regardless if they are a slave of the master.

To connect to a server, it is necessary to specify connection parameters such as user name, host name, password, and either a port or socket. MySQL Utilities provides a number of ways to supply this information. All of the methods require specifying your choice via a command-line option such as --server, --master, --slave, etc. The methods include the following in order of most secure to least secure.

Use login-paths from your .mylogin.cnf file (encrypted, not visible). Example : <login-path>[:<port>][:<socket>]

Use a configuration file (unencrypted, not visible) Note: available in release-1.5.0. Example : <configuration-file-path>[:<section>]

Specify the data on the command-line (unencrypted, visible). Example : <user>[:<passwd>]@<host>[:<port>][:<socket>]

 --ssl-ca

The path to a file that contains a list of trusted SSL CAs.

 --ssl-cert

The name of the SSL certificate file to use for establishing a secure connection.

 --ssl-key

The name of the SSL key file to use for establishing a secure connection.

 --ssl

Specifies if the server connection requires use of SSL. If an encrypted connection cannot be established, the connection attempt fails. Default setting is 0 (SSL not required).

 --timeout=<seconds>

Maximum timeout in seconds to wait for each replication command to complete. For example, timeout for slave waiting to catch up to master.

Default = 3.

 --verbose, -v

Specify how much information to display. Use this option multiple times to increase the amount of information. For example, -v = verbose, -vv = more verbose, -vvv = debug.

 --version

Display version information and exit.

NOTES

The login user must have the appropriate permissions for the utility to check servers and monitor their status (e.g., SHOW SLAVE STATUS, SHOW MASTER STATUS). The user must also have permissions to execute the failover procedure (e.g., STOP SLAVE, START SLAVE, WAIT_UNTIL_SQL_THREAD_AFTER_GTIDS, CHANGE MASTER TO ...). Lastly, the user must have the REPLICATE SLAVE privilege for slaves to connect to their master. The same permissions are required by the failover utility for master and slaves in order to run successfully. In particular, users connected to slaves, candidates and master require SUPER, GRANT OPTION, REPLICATION SLAVE, RELOAD, DROP, CREATE, INSERT and SELECT privileges.

The DROP, CREATE, INSERT and SELECT privileges are required to register the failover instance on the initial master or the new master (after a successful failover). Therefore, since any slave can become the new master, slaves and candidates also require those privileges. The utility checks permissions for the master, slaves, and candidates at startup.
```
