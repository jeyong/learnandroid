# Concurrency

## Executor
 * 받은 Runnable task를 실행하는 객체
 * 각 task의 실행 방법과(thread, scheduling, ...) task를 분리
```java
Executor executor = exec();
exec.execute(new RunnableTask1());
exec.execute(new RunnableTask2());
```
 * 비동기를 강제하지는 않음
 * caller의 thread에서 바로 실행도 가능
```java
class DirectorExecutor implements Executor {
    public void execute(Runnable r){
        r.run()
    }
}
```
 * 가장 일반적인 경우는 caller의 thread가 아닌 다른 thread로 실행하는 경우
```java
class ThreadPerTaskExecutor implements Executor {
    public void execute(Runnable r) {
        new Thread(r).start();
    }
}
```
 * 구현시 실행 방법과 스케줄링에 대한 제한
```java
class SerialExecutor implements Executor {
    final Queue<Runnable> tasks = new ArrayDque<>();
    final Executor executor;
    Runnable active;

    SerialExecutor(Executor executor) {
        this.executor = exector;
    }

    public synchronized void execute(final Runnable r) {
        tasks.add(new Runnable) {
            public void run() {
                try{
                    r.run();
                } finally {
                    scheduleNext();
                }
            }
        });
        if (active == null) {
            sheducleNext();
        }
    }

    protected synchronized void scheduleNext() {
        if ((active = tasks.poll()) != null) {
            executor.execute(active);
        }
    }
}
```
