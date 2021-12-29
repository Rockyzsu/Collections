# mongodb意外断电,非正常关闭, 造成不可启动, 日志出现WT_ERROR: non-specific WiredTiger error, terminating



# 亲测





 今天启动MongoDB, /**/mongod -f /**/mongodb.conf

 今天服务器突然都断电了, 我重新启动的时候, 已经启动不成功, 去log文件夹下面, 看了一下日志: 

```
2020-12-28T12:51:29.423+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2020-12-28T12:51:29.423+0800 I CONTROL  [initandlisten] options: { config: "/home/**/mongodb/conf/mongodb.conf", net: { port: 27017 }, processManagement: { fork: true, pidFilePath: "/home/**/mongodb/data/mongodb.pid" }, repair: true, replication: { oplogSizeMB: 512 }, storage: { dbPath: "/home/**/mongodb/data/" }, systemLog: { destination: "file", logAppend: true, path: "/home/**/mongodb/log/mongodb.log" } }
2020-12-28T12:51:29.449+0800 E NETWORK  [initandlisten] listen(): bind() failed No space left on device for socket: /tmp/mongodb-27017.sock
2020-12-28T12:51:29.449+0800 E NETWORK  [initandlisten] Failed to set up sockets during startup.
2020-12-28T12:51:29.449+0800 E STORAGE  [initandlisten] Failed to set up listener: InternalError: Failed to set up sockets
2020-12-28T12:51:29.449+0800 I NETWORK  [initandlisten] shutdown: going to close listening sockets...
2020-12-28T12:51:29.449+0800 I NETWORK  [initandlisten] shutdown: going to flush diaglog...
2020-12-28T12:51:29.449+0800 I CONTROL  [initandlisten] now exiting
2020-12-28T12:51:29.449+0800 I CONTROL  [initandlisten] shutting down with code:48
2020-12-28T13:03:26.708+0800 I CONTROL  [main] ***** SERVER RESTARTED *****
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] MongoDB starting : pid=110233 port=27017 dbpath=/home/**/mongodb/data/ 64-bit host=localhost.localdomain
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] db version v3.4.3
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] git version: f07437fb5a6cca07c10bafa78365456eb1d6d5e1
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.0-fips 29 Mar 2010
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] allocator: tcmalloc
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] modules: none
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] build environment:
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten]     distmod: amazon
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten]     distarch: x86_64
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2020-12-28T13:03:26.713+0800 I CONTROL  [initandlisten] options: { config: "/home/**/mongodb/conf/mongodb.conf", net: { port: 27017 }, processManagement: { fork: true, pidFilePath: "/home/**/mongodb/data/mongodb.pid" }, repair: true, replication: { oplogSizeMB: 512 }, storage: { dbPath: "/home/**/mongodb/data/" }, systemLog: { destination: "file", logAppend: true, path: "/home/**/mongodb/log/mongodb.log" } }
2020-12-28T13:03:26.737+0800 E NETWORK  [initandlisten] listen(): bind() failed No space left on device for socket: /tmp/mongodb-27017.sock
2020-12-28T13:03:26.737+0800 E NETWORK  [initandlisten] Failed to set up sockets during startup.
2020-12-28T13:03:26.737+0800 E STORAGE  [initandlisten] Failed to set up listener: InternalError: Failed to set up sockets
2020-12-28T13:03:26.737+0800 I NETWORK  [initandlisten] shutdown: going to close listening sockets...
2020-12-28T13:03:26.737+0800 I NETWORK  [initandlisten] shutdown: going to flush diaglog...
2020-12-28T13:03:26.737+0800 I CONTROL  [initandlisten] now exiting
2020-12-28T13:03:26.737+0800 I CONTROL  [initandlisten] shutting down with code:48
```

我看到了listen(): bind() failed No space left on device for socket: /tmp/mongodb-27017.sock, 这句话, 说明磁盘空间不够, df -h, 看了一下, 确实是空间不够, 清理完之后, 接着重新启动, 又失败:

```
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] MongoDB starting : pid=8356 port=27017 dbpath=/home/**/mongodb/data/ 64-bit host=localhost.localdomain
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] db version v3.4.3
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] git version: f07437fb5a6cca07c10bafa78365456eb1d6d5e1
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.0-fips 29 Mar 2010
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] allocator: tcmalloc
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] modules: none
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] build environment:
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten]     distmod: amazon
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten]     distarch: x86_64
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2020-12-28T19:04:49.385+0800 I CONTROL  [initandlisten] options: { config: "/home/**/mongodb/conf/mongodb.conf", net: { port: 27017 }, processManagement: { fork: true, pidFilePath: "/home/**/mongodb/data/mongodb.pid" }, repair: true, replication: { oplogSizeMB: 512 }, storage: { dbPath: "/home/**/mongodb/data/" }, systemLog: { destination: "file", logAppend: true, path: "/home/**/mongodb/log/mongodb.log" } }
2020-12-28T19:04:49.414+0800 I -        [initandlisten] Detected data files in /home/**/mongodb/data/ created by the 'wiredTiger' storage engine, so setting the active storage engine to 'wiredTiger'.
2020-12-28T19:04:49.414+0800 I STORAGE  [initandlisten] Detected WT journal files.  Running recovery from last checkpoint.
2020-12-28T19:04:49.414+0800 I STORAGE  [initandlisten] journal to nojournal transition config: create,cache_size=15557M,session_max=20000,eviction=(threads_min=4,threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,archive=true,path=journal,compressor=snappy),file_manager=(close_idle_time=100000),checkpoint=(wait=60,log_size=2GB),statistics_log=(wait=0),
2020-12-28T19:04:49.436+0800 E STORAGE  [initandlisten] WiredTiger error (-31802) [1609153489:436086][8356:0x7fd6498a2e00], txn-recover: unsupported WiredTiger file version: this build  only supports major/minor versions up to 1/0,  and the file is version 2/0: WT_ERROR: non-specific WiredTiger error
2020-12-28T19:04:49.436+0800 E STORAGE  [initandlisten] WiredTiger error (0) [1609153489:436137][8356:0x7fd6498a2e00], txn-recover: WiredTiger is unable to read the recovery log.
2020-12-28T19:04:49.436+0800 E STORAGE  [initandlisten] WiredTiger error (0) [1609153489:436146][8356:0x7fd6498a2e00], txn-recover: This may be due to the log files being encrypted, being from an older version or due to corruption on disk
2020-12-28T19:04:49.436+0800 E STORAGE  [initandlisten] WiredTiger error (0) [1609153489:436152][8356:0x7fd6498a2e00], txn-recover: You should confirm that you have opened the database with the correct options including all encryption and compression options
2020-12-28T19:04:49.436+0800 E STORAGE  [initandlisten] WiredTiger error (-31802) [1609153489:436163][8356:0x7fd6498a2e00], txn-recover: Recovery failed: WT_ERROR: non-specific WiredTiger error
2020-12-28T19:04:49.436+0800 I -        [initandlisten] Assertion: 28718:-31802: WT_ERROR: non-specific WiredTiger error src/mongo/db/storage/wiredtiger/wiredtiger_kv_engine.cpp 251
2020-12-28T19:04:49.438+0800 I STORAGE  [initandlisten] exception in initAndListen: 28718 -31802: WT_ERROR: non-specific WiredTiger error, terminating
2020-12-28T19:04:49.438+0800 I NETWORK  [initandlisten] shutdown: going to close listening sockets...
2020-12-28T19:04:49.438+0800 I NETWORK  [initandlisten] removing socket file: /tmp/mongodb-27017.sock
2020-12-28T19:04:49.438+0800 I NETWORK  [initandlisten] shutdown: going to flush diaglog...
2020-12-28T19:04:49.438+0800 I CONTROL  [initandlisten] now exiting
2020-12-28T19:04:49.438+0800 I CONTROL  [initandlisten] shutting down with code:100
2020-12-28T19:06:07.035+0800 I CONTROL  [main] ***** SERVER RESTARTED *****
```

 上面由于不正常关机, 造成数据库被锁起来了, 需要去db目录下面:

```
cd /data/db    //进入数据文件夹
rm -r journal 
rm -r mongod.lock 
rm -r WiredTiger.lock
```

然后接着重启服务就可以了