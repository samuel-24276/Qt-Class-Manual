# QThread

# 1.Detailed Description

一个QThread对象 管理程序中的一个控制线程。 QThreads开始在run（）中执行。 **默认情况下，run（）通过调用exec（）启动事件循环，并在线程内部运行Qt事件循环。**

方法一：您可以通过使用QObject :: moveToThread（）将辅助对象移动到线程来使用辅助对象。

```c++
 class Worker : public QObject
 {
     Q_OBJECT

 public slots:
     void doWork(const QString &parameter) {
         QString result;
         /* ... here is the expensive or blocking operation ... */
         emit resultReady(result);
     }

 signals:
     void resultReady(const QString &result);
 };

 class Controller : public QObject
 {
     Q_OBJECT
     QThread workerThread;
 public:
     Controller() {
         Worker *worker = new Worker;
         worker->moveToThread(&workerThread);
         connect(&workerThread, &QThread::finished, worker, &QObject::deleteLater);
         connect(this, &Controller::operate, worker, &Worker::doWork);
         connect(worker, &Worker::resultReady, this, &Controller::handleResults);
         workerThread.start();
     }
     ~Controller() {
         workerThread.quit();
         workerThread.wait();
     }
 public slots:
     void handleResults(const QString &);
 signals:
     void operate(const QString &);
 };
```

然后，Worker slot中的代码将在单独的线程中执行。 但是，您可以自由地将Worker的slot连接到任何线程中来自任何对象的任何信号。 借助一种称为队列连接的机制，可以安全地跨不同线程连接信号和槽。
方法二：子类QThread和重新实现run（）。 例如：

```c++
 class WorkerThread : public QThread
 {
     Q_OBJECT
     void run() override {
         QString result;
         /* ... here is the expensive or blocking operation ... */
         emit resultReady(result);
     }
 signals:
     void resultReady(const QString &s);
 };

 void MyObject::startWorkInAThread()
 {
     WorkerThread *workerThread = new WorkerThread(this);
     connect(workerThread, &WorkerThread::resultReady, this, &MyObject::handleResults);
     connect(workerThread, &WorkerThread::finished, workerThread, &QObject::deleteLater);
     workerThread->start();
 }
```

在该示例中，线程将在run函数返回后退出。**除非您调用exec（），否则线程中不会运行任何事件循环**。
重要的是要记住，**QThread实例存在于实例化它的旧线程中，而不是存在于调用run（）的新线程中**。这意味着所有QThread队列里的slot和调用的方法都将在旧线程中执行。因此，**希望在新线程中调用slot开发人员必须使用工作对象方法。新的slot不应直接实现到子类QThread中**。
与排队的slot或调用的方法不同，直接在QThread对象上调用的方法将在调用该方法的线程中执行。**子类化QThread时，请记住，构造函数在旧线程中执行，而run（）在新线程中执行。如果从两个函数访问成员变量，则将从两个不同的线程访问该变量。检查这样做是否安全**。
注意：在跨不同线程与对象进行交互时，必须小心。有关详细信息，请参见Synchronizing Threads。

# 2.Managing Threads

- 当线程是started（）或finished（）时，QThread会通过信号通知您，或者您可以使用isFinished（）和isRunning（）来查询线程的状态。
- 您可以通过调用exit（）或quit（）来停止线程。 在极端情况下，您可能需要强制终止执行线程。 但是，这样做是危险的，不鼓励这样做。 请阅读terminate（）和setTerminationEnabled（）的文档以获取详细信息。
- 从Qt 4.8开始，**可以通过将finish（）信号连接到QObject :: deleteLater（）来释放生活在刚刚结束的线程中的对象**。
- **使用wait（）阻止调用线程，直到另一个线程完成执行（或直到经过指定的时间）为止**。
- QThread还提供了与平台无关的静态睡眠函数：sleep（），msleep（）和usleep（）分别允许完整的秒，毫秒和微秒的分辨率。 这些功能已在Qt 5.0中公开。

Node：通常，因为Qt是事件驱动的框架，所以通常不需要使用wait（）和sleep（）函数。代替wait（），可以考虑侦听finished（）信号。考虑使用QTimer，而不是sleep（）函数。

- 静态函数currentThreadId（）和currentThread（）返回当前正在执行的线程的标识符。 **前者返回线程的特定于平台的ID。 后者返回一个QThread指针**。
- 要选择将给您的线程指定的名称（例如，在Linux上由命令ps -L标识），可以在启动线程之前调用`setObjectName（）`。 **如果不调用setObjectName（），则为线程提供的名称将是线程对象的运行时类型的类名**（例如，对于Mandelbrot Example，为“ RenderThread”，因为它是 QThread子类）。* 请注意，这在Windows上的发行版中当前不可用*。

# 3.Member Type Documentation

enum QThread::Priority

此枚举类型指示操作系统应如何调度新创建的线程。

| Constant                      | Value | Description                                                  |
| ----------------------------- | ----- | ------------------------------------------------------------ |
| QThread::IdlePriority         | 0     | scheduled only when no other threads are running.            |
| QThread::LowestPriority       | 1     | scheduled less often than LowPriority.                       |
| QThread::LowPriority          | 2     | scheduled less often than NormalPriority.                    |
| QThread::NormalPriority       | 3     | the default priority of the operating system.                |
| QThread::HighPriority         | 4     | scheduled more often than NormalPriority.                    |
| QThread::HighestPriority      | 5     | scheduled more often than HighPriority.                      |
| QThread::TimeCriticalPriority | 6     | scheduled as often as possible.                              |
| QThread::InheritPriority      | 7     | use the same priority as the creating thread. This is the default. |

# 4.Member Function Documentation

## 4.1.构造函数

`QThread::QThread(QObject *parent = nullptr)`

构造一个新的QThread来管理一个新线程。 parent拥有QThread的所有权。 在调用start（）之前，线程不会开始执行。

## 4.2.信号finished()

`[signal] void QThread::finished()`

- 该信号在执行完成之前立即从关联线程发出。
- 发出此信号时，事件循环已经停止运行。 除了延迟的删除事件外，线程中将不再处理其他事件。 该信号可以连接到`QObject :: deleteLater（）`，以释放该线程中的对象。
- 注意：如果使用`terminate（）`终止了关联的线程，则不确定从哪个线程发出该信号。
- 注意：这是一个private信号。 它**可以用于信号连接，但不能由用户发射**。

## 4.3.槽函数quit()

`[slot] void QThread::quit()`

告诉线程的事件循环以返回码0（成功）退出。 等效于调用QThread :: exit（0）。

如果线程没有事件循环，则此函数不执行任何操作。

## 4.4.槽函数start()

`[slot] void QThread::start(QThread::Priority priority = InheritPriority)`

通过调用`run（）`开始执行线程。 操作系统将根据priority参数调度线程。 如果线程已经在运行，则此功能不执行任何操作。

priority *参数的作用取决于操作系统的调度策略。 特别是，在不支持线程优先级的系统上（例如，在Linux上，）* priority 将被忽略。

## 4.5.信号started()

`[signal] void QThread::started()`

在调用run（）函数之前，该信号在开始执行时从关联线程发出。
注意：这是一个private信号。 它可以用于信号连接，但不能由用户发射。

## 4.6.槽函数terminate()

`[slot] void QThread::terminate()`

终止线程的执行。根据操作系统的调度策略，线程可能会立即终止，也可能不会立即终止。可以在终止（）之后使用`QThread :: wait()`。

当线程终止时，所有等待线程完成的线程都将被唤醒。

**警告：此功能很危险，不建议使用。 线程可以在其代码路径中的任何位置终止。 修改数据时可以终止线程。 线程自身无法清除，解锁任何保持的互斥锁等。总之，仅在绝对必要时才使用此功能。**

可以通过调用`QThread :: setTerminationEnabled（）`显式启用或禁用Termination 。 在禁用终止的情况下调用此函数会导致Termination 延迟，直到重新启用终止为止。

## 4.7.静态函数currentThread()

`[static] QThread *QThread::currentThread()`

返回指向管理当前执行线程的QThread的指针。

`[static] Qt::HANDLE QThread::currentThreadId()`

返回当前执行线程的线程句柄。

警告：此函数返回的句柄仅供内部使用，不应在任何应用程序代码中使用。

注意：在Windows上，此函数返回Win32函数GetCurrentThreadId（）返回的DWORD（Windows线程ID），而不是Win32函数GetCurrentThread（）返回的伪HANDLE（Windows线程处理）。

## 4.8.重写的虚函数event（）

`[override virtual] bool QThread::event(QEvent *event)`

该函数接收到对象事件，如果识别并处理了事件event，则应返回true。

## 4.9.线程的事件调度函数eventDispatcher()

`QAbstractEventDispatcher *QThread::eventDispatcher() const`

返回指向线程的事件调度程序对象的指针。 如果该线程不存在事件分派器，则此函数返回nullptr。

此功能在Qt 5.0中引入。

## 4.10.事件循环函数exec()

`[protected] int QThread::exec()`

进入事件循环并等待，直到调用exit（），然后返回传递给exit（）的值。 如果通过quit（）调用exit（），则返回的值为0。

**该函数应在run（）中调用。 必须调用此函数来开始事件处理**。

## 4.11.exit()函数

`void QThread::exit(int returnCode = 0)`

告诉线程的事件循环以返回码退出。

调用此函数后，线程离开事件循环，并从调用返回到`QEventLoop :: exec（）`。 `QEventLoop :: exec（）`函数返回returnCode 。

按照惯例，returnCode 为0表示成功，任何非零值都表示错误。

请注意，与同名的C库函数不同，此函数“确实”返回到调用者-事件处理停止。

在再次调用`QThread :: exec（）`之前，不会在此线程中启动任何QEventLoops。 如果QThread :: exec（）`中的事件循环未运行，则对`QThread :: exec（）的下一次调用也将立即返回。

## 4.12.静态函数sleep()

`[static] void QThread::sleep(unsigned long secs)`

**强制当前线程休眠secs秒**。

如果需要等待给定条件的改变，请避免使用此功能。 而是将槽连接到指示更改的信号或使用事件处理程序（请参见`QObject :: event（）`）。

注意：此功能不保证准确性。 在重负载条件下，应用程序的睡眠时间可能超过sec 。

## 4.13.wait()函数

`bool QThread::wait(unsigned long time)`

这是一个重载函数

`bool QThread::wait(QDeadlineTimer deadline = QDeadlineTimer(QDeadlineTimer::Forever))`

阻塞线程，直到满足以下任一条件：

- 与此QThread对象关联的线程已完成执行（即，当它从run（）返回时）。 如果线程完成，此函数将返回true。 如果线程尚未启动，它也会返回true。
- 截止日期已到。 如果到了最后期限，此函数将返回false。

设置为QDeadlineTimer :: Forever（默认值）的截止期限计时器永远不会超时：在这种情况下，该函数仅在线程从run（）返回或线程尚未启动时才返回。

# 5.各类错误

- 1. QTcpSocket对象创建和使用要在同一个线程，否则报错。 

     错误描述：`QObject: Cannot create children for a parent that is in a different thread.`

     QObject：无法为处于不同线程中的父级创建子级。

- 2.disconnectFromHost()和waitForDisconnected()配合使用，没有数据读入则直接断开客户端

  错误描述：`QAbstractSocket::waitForDisconnected() is not allowed in UnconnectedState`

# 6.Public Functions

```c++
QThread(QObject *parent = nullptr)
virtual ~QThread()
QAbstractEventDispatcher * eventDispatcher() const	//事件调度
void exit(int returnCode = 0)						//线程退出
bool isFinished() const								
bool isInterruptionRequested() const
bool isRunning() const
int loopLevel() const
QThread::Priority priority() const
void requestInterruption()
void setEventDispatcher(QAbstractEventDispatcher *eventDispatcher)
void setPriority(QThread::Priority priority)
void setStackSize(uint stackSize)
uint stackSize() const
bool wait(QDeadlineTimer deadline = QDeadlineTimer(QDeadlineTimer::Forever))
bool wait(unsigned long time)

```

# 7.Reimplemented Public Functions

```c++
virtual bool event(QEvent *event) override
```

# 8.Public Slots

```c++
void quit()
void start(QThread::Priority priority = InheritPriority)
void terminate()
```

# 9.Signals

```c++
void finished()
void started()
```

# 10.Static Public Members

```c++
QThread * create(Function &&f, Args &&... args)
QThread * create(Function &&f)
QThread * currentThread()
Qt::HANDLE currentThreadId()
int idealThreadCount()
void msleep(unsigned long msecs)
void sleep(unsigned long secs)
void usleep(unsigned long usecs)
void yieldCurrentThread()
```

# 11.Protected Functions

```c++
int exec()
virtual void run()
```

# 12.Static Protected Members

```c++
void setTerminationEnabled(bool enabled = true)
```







