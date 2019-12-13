---
layout:     post
title:      StopWatch
subtitle:   StopWatch
date:       2019-12-13            
author:     小康kangs                
header-img: img/post-bg-coffee.jpg
catalog: 	  true
tags:
   - StopWatch
        
---



#####            程序中需要查看某个方法的执行时间，一般情况下可能就使用方法开始时获取当前时间，方法结束以后再获取当前时间，然后两个时间相减就可 以获得 间隔时间，间隔 时间就是 方法的执行时间啦（没错这就是我本人了/(ㄒoㄒ)/~~)。

​         But看到了一个类**StopWatch**，这个类集成了获取方法执行时间相关的方法，

```java
    public static void main(String[] args) throws InterruptedException {
        StopWatch watch = new StopWatch("获取方法执行时间");
        StopWatch watchs = new StopWatch("获取方法循环执行时间");
        logger.info(watch.getId());
        watch.start("执行一次时间");
        Thread.sleep(1000); // 暂停一秒
        watch.stop();

        for (int i = 0; i < 5; i++) {
            watchs.start("循环执行时间");
            Thread.sleep(1000); // 暂停一秒
            watchs.stop();
        }
        logger.info("{}，执行时间{}ms，执行次数{}次", watch.getId(), watch.getTotalTimeMillis(), watch.getTaskCount());
        logger.info("{}，执行时间{}ms，{}s，执行次数{}次", watchs.getId(), watchs.getTotalTimeMillis(),
                watchs.getTotalTimeSeconds(), watchs.getTaskCount());
        logger.info("{}，最后一次执行时间{}ms", watchs.getId(), watchs.getLastTaskTimeMillis());
    }
```

```java
[15:40:59.060] INFO  com.example.lbyanBack.util.SystemUtil 35 main - 获取方法执行时间
[15:41:05.086] INFO  com.example.lbyanBack.util.SystemUtil 45 main - 获取方法执行时间，执行时间1000ms，执行次数1次
[15:41:05.087] INFO  com.example.lbyanBack.util.SystemUtil 46 main - 获取方法循环执行时间，执行时间5002ms，5.002s，执行次数5次
[15:41:05.088] INFO  com.example.lbyanBack.util.SystemUtil 48 main - 获取方法循环执行时间，最后一次执行时间1000ms

```

方法可以获取执行的时间,执行的次数，总时间，最后一次执行时间等