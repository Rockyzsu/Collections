使用事务:

以begin开头





### 隔离级别

```
SELECT @@tx_isolation;
```

得到

> REPEATABLE-READ

默认是可重复读



```
SELECT @@global.tx_isolation; //全局
```

