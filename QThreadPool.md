# QThreadPool

# 1.Detailed Description

QThreadPool管理和回收单个QThread对象，以帮助减少使用线程的程序中的线程创建成本。 每个Qt应用程序都有一个全局QThreadPool对象，可以通过调用`globalInstance（）`来访问该对象。
要使用QThreadPool线程之一，请子类QRunnable并实现run（）虚拟函数。 然后创建该类的对象，并将其传递给`QThreadPool :: start（）`。

```c++
 class HelloWorldTask : public QRunnable
 {
     void run() override
     {
         qDebug() << "Hello world from thread" << QThread::currentThread();
     }
 };

 HelloWorldTask *hello = new HelloWorldTask();
 // QThreadPool takes ownership and deletes 'hello' automatically
 QThreadPool::globalInstance()->start(hello);
```

QThreadPool默认情况下会自动删除QRunnable。使用`QRunnable :: setAutoDelete（）`更改自动删除标志。
QThreadPool通过在`QRunnable :: run（）`中调用tryStart（this）支持多次执行同一QRunnable。如果启用了autoDelete，则当最后一个线程退出运行功能时，QRunnable将被删除。**启用autoDelete时，使用相同的QRunnable多次调用start（）会创建竞争条件，因此不建议这样做**。

在一定时间内未使用的线程将过期(expire)。 默认的过期超时为30000毫秒（30秒）。 可以使用`setExpiryTimeout（）`进行更改。 设置负的到期超时将禁用到期机制。
调用`maxThreadCount（）`以查询要使用的最大线程数。 如果需要，可以使用`setMaxThreadCount（）`更改限制。 **默认的maxThreadCount（）是QThread :: idealThreadCount（）**。 `activeThreadCount（）`函数返回当前正在工作的线程数。
`reserveThread（）`函数保留一个线程供外部使用。 处理完线程后，请使用`releaseThread（）`，以便可以重用它。 本质上，这些函数会暂时增加或减少活动线程数，并且在实现QThreadPool不可见的耗时操作时很有用。
请注意，**QThreadPool是用于管理线程的低级类**，有关更高级的选择，请参阅Qt Concurrent模块。

# 2.Properties

- activeThreadCount : const int

  表示线程池中活动线程的数量。

- expiryTimeout : int

  在expiryTimeout毫秒内未使用的线程将被视为已过期并将退出。 **此类线程将根据需要重新启动**。 默认的expiryTimeout为30000毫秒（30秒）。 如果expiryTimeout为负数，则新创建的线程将不会过期，例如，直到销毁线程池后，它们才会退出。

  请注意，**设置expiryTimeout对已经运行的线程无效**。 仅新创建的线程将使用新的expiryTimeout。 我们建议**在创建线程池之后但在调用start（）之前立即设置expiryTimeout**。

- maxThreadCount : int

  此属性表示线程池使用的最大线程数。
  注意：即使maxThreadCount限制为零或负数，线程池将始终至少使用1个线程。
  默认的maxThreadCount是QThread :: idealThreadCount（）。

- stackSize : uint 

  此属性包含线程池工作线程的堆栈大小。
  该属性的值仅在线程池创建新线程时使用。 更改它对已创建或正在运行的线程无效。
  默认值为0，这使QThread使用操作系统的默认堆栈大小。

# 3.Public Functions

- QThreadPool(QObject *parent = nullptr)

- virtual ~QThreadPool()

- void clear()

  从队列中删除尚未启动的可运行对象。 runnable-> autoDelete（）返回true的runnable被删除。

- **void releaseThread()**

  **释放先前通过调用reserveThread（）保留的线程**。
  注意：在不事先保留线程的情况下调用此函数会临时增加maxThreadCount（）。 当线程进入睡眠状态以等待更多工作，从而允许其他线程继续运行时，此功能很有用。 请确保在完成等待后调用reserveThread（），以便线程池可以正确维护activeThreadCount（）。

- **void reserveThread()**

  **保留一个线程，而不考虑activeThreadCount（）和maxThreadCount（）。**
  **一旦完成线程处理，请调用releaseThread（）以允许其重用**。
  注意：此功能将始终增加活动线程的数量。 这意味着通过使用此函数，activeThreadCount（）可以返回大于maxThreadCount（）的值。

- void setExpiryTimeout(int expiryTimeout)

- void setMaxThreadCount(int maxThreadCount)

- void setStackSize(uint stackSize)

- void start(QRunnable *runnable, int priority = 0)

  **保留线程并使用它run可运行的对象，除非该线程使当前线程数超过maxThreadCount（）**。 在这种情况下，将runnable添加到运行队列中。 priority参数可用于控制运行队列的执行顺序。
  请注意，如果runnable-> autoDelete（）返回true，则线程池将获得runnable的所有权，并且在runnable-> run（）返回之后，线程池将自动删除该runnable。 如果runnable-> autoDelete（）返回false，则调用者将保留runnable的所有权。 请注意，在调用此函数后更改runnable的自动删除将导致未定义的行为。

- void start(std::function<void ()> functionToRun, int priority = 0)

  保留一个线程并使用它运行functionToRun，除非该线程将使当前线程数超过maxThreadCount（）。 在这种情况下，将functionToRun添加到运行队列中。 priority参数可用于控制运行队列的执行顺序

- bool tryStart(QRunnable *runnable)

  尝试保留线程以运行runnable。
  如果在调用时没有线程可用，则此函数不执行任何操作并返回false。 否则，将使用一个可用线程立即运行runnable，并且此函数返回true。
  请注意，如果runnable-> autoDelete（）返回true，则线程池成功获取runnable的所有权，并且在runnable-> run（）返回之后，线程池将自动删除该runnable。 如果runnable-> autoDelete（）返回false，则调用者将保留runnable的所有权。 请注意，在调用此函数后更改runnable的自动删除将导致未定义的行为。

- bool tryStart(std::function<void ()> functionToRun)

  尝试保留线程以运行functionToRun。
  如果在调用时没有线程可用，则此函数不执行任何操作并返回false。 否则，functionToRun将使用一个可用线程立即运行，并且此函数返回true。

- bool tryTake(QRunnable *runnable)

- bool waitForDone(int msecs = -1)

  等待所有毫秒退出（以毫秒为单位），然后从线程池中删除所有线程。 如果删除了所有线程，则返回true；否则，返回true。 否则返回false。 如果毫秒为-1（默认值），则忽略超时（等待最后一个线程退出）。

# 4.Static Public Members

`QThreadPool *globalInstance()` 返回全局的线程池实例