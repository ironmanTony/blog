title: AysncTask源码解析
date: 2015-08-06 16:03:13
tags:
---

## AsyncTask的类图

![](/imgs/asynctask.png)

* 其中，如果使用默认的Executor其实AsyncTask中的任务是一个一个执行的。
其中灰色的是接口

```
    private static class SerialExecutor implements Executor {
        final ArrayDeque<Runnable> mTasks = new ArrayDeque<Runnable>();
        Runnable mActive;

        public synchronized void execute(final Runnable r) {
            mTasks.offer(new Runnable() {
                public void run() {
                    try {
                        r.run();
                    } finally {
                        scheduleNext();
                    }
                }
            });
            if (mActive == null) {
                scheduleNext();
            }
        }

        protected synchronized void scheduleNext() {
            if ((mActive = mTasks.poll()) != null) {
                THREAD_POOL_EXECUTOR.execute(mActive);
            }
        }
    }
```

从这段代码中可以看出来。     
如果使用Thread_pool_executor那么就会使用线程池来执行你的task。
注释中也有：

Order of execution

When first introduced, AsyncTasks were executed serially on a single background
thread. Starting with {android.os.Build.VERSION_CODES#DONUT}, this was changed
to a pool of threads allowing multiple tasks to operate in parallel. Starting with
android.os.Build.VERSION_CODES#HONEYCOMB, tasks are executed on a single
thread to avoid common application errors caused by parallel execution

 If you truly want parallel execution, you can invoke
executeOnExecutor(java.util.concurrent.Executor, Object[])} with
THREAD_POOL_EXECUTOR

* 从类图可以看出来AsyncTask主要使用了组合的方式来使用代码。

* 理解代码的一个方式是画类图，然后找一个入口然后看下去，看他是如何调用的。

