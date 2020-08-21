# QMutex

# 1.Detailed Description

QMutex的目的是保护对象，数据结构或代码段，以便一次只能有一个线程可以访问它（这类似于Java sync关键字）。 通常最好将互斥锁与QMutexLocker一起使用，因为这样可以轻松确保一致地执行锁定和解锁。
例如，假设有一种方法可以在两行上向用户打印一条消息：

```c++
 int number = 6;

 void method1()
 {
     number *= 5;
     number /= 4;
 }

 void method2()
 {
     number *= 3;
     number /= 2;
 }
```

如果连续调用这两个方法，则会发生以下情况：

```c++
 // method1()
 number *= 5;        // number is now 30
 number /= 4;        // number is now 7

 // method2()
 number *= 3;        // number is now 21
 number /= 2;        // number is now 10
```

如果从两个线程同时调用这两个方法，则可能会导致以下顺序：

```c++
 // Thread 1 calls method1()
 number *= 5;        // number is now 30

 // Thread 2 calls method2().
 //
 // Most likely Thread 1 has been put to sleep by the operating
 // system to allow Thread 2 to run.
 number *= 3;        // number is now 90
 number /= 2;        // number is now 45

 // Thread 1 finishes executing.
 number /= 4;        // number is now 11, instead of 10
```

如果添加互斥锁，则应获得所需的结果：

```c++
QMutex mutex;
 int number = 6;

 void method1()
 {
     mutex.lock();
     number *= 5;
     number /= 4;
     mutex.unlock();
 }

 void method2()
 {
     mutex.lock();
     number *= 3;
     number /= 2;
     mutex.unlock();
 }
```

那么在任何给定时间只有一个线程可以修改数字，并且结果是正确的。 当然，这是一个简单的示例，但适用于需要按特定顺序发生的任何其他情况。
**当您在线程中调用lock（）时，其他尝试在同一位置调用lock（）的线程将阻塞，直到获得锁的线程调用unlock（）为止**。 tryLock（）是lock（）的一种非阻塞替代方法。
QMutex经过优化，可以在非竞争情况下快速运行。 如果该互斥锁上没有争用，则非递归QMutex将不会分配内存。 它的构建和销毁几乎没有开销，这意味着可以将许多互斥锁作为其他类的一部分。

# 2.Public Types

`enum RecursionMode { Recursive, NonRecursive }`枚举类型，递归模式，有递归和非递归两种。

# 3.Public Functions

- `QMutex(QMutex::RecursionMode mode)`

  构造一个新的互斥量。 互斥锁以解锁状态创建。
  **如果mode为`QMutex :: Recursive`，则线程可以多次锁定同一个互斥锁，并且只有在进行了相应数量的unlock（）调用后，该互斥锁才会被解锁**。 否则，一个线程只能锁定一个互斥锁一次。 默认值为QMutex :: NonRecursive。
  与非递归互斥锁相比，递归互斥锁较慢并且占用更多内存。

- `QMutex()`

- `~QMutex()`

- `bool isRecursive() const`

  如果互斥量是递归的，则返回true。

- `void lock()`

  锁定互斥锁。 如果另一个线程锁定了互斥锁，则该调用将一直阻塞，直到该线程将其解锁为止。
  **如果此互斥锁是递归互斥锁，则允许在同一线程的同一互斥锁上多次调用此函数**。 如果此互斥锁是非递归互斥锁，则此功能将在递归锁定互斥锁时死锁。

- `bool tryLock(int timeout = 0)`

  尝试锁定互斥锁。 如果获得了锁，则此函数返回true；否则，返回false。 如果另一个线程锁定了互斥锁，则此功能将最多等待超时毫秒timeout以使该互斥锁可用。
  注意：**由于超时而传递负数等效于调用lock（），即如果超时为负，则此函数将永远等待直到互斥锁可以被锁定为止**。
  如果获得了锁定，则互斥锁必须在另一个线程成功锁定之前使用unlock（）进行解锁。
  如果此互斥锁是递归互斥锁，则允许在同一线程的同一互斥锁上多次调用此函数。 如果此互斥锁是非递归互斥锁，则在尝试递归锁定互斥锁时，此函数将始终返回false。

- `bool try_lock()`

  尝试锁定互斥锁。 如果获得了锁，则此函数返回true；否则，返回false。 
  提供此功能是为了与标准库概念“可锁定”兼容。 它等效于tryLock（）。
  如果获得了锁定，则该函数返回true； 否则返回false。

- `bool try_lock_for(std::chrono::duration<Rep, Period> duration)`

  尝试锁定互斥锁。 如果获得了锁，则此函数返回true；否则，返回false。如果另一个线程锁定了互斥锁，则此功能将至少等待一段时间才能使该互斥锁可用。
  注意：传递负数的持续时间，因为持续时间等效于调用try_lock（）。 此行为不同于tryLock（）。
  如果获得了锁定，则互斥锁必须在另一个线程成功锁定之前使用unlock（）进行解锁。
  如果此互斥锁是递归互斥锁，则允许在同一线程的同一互斥锁上调用此时间。 如果此互斥锁是非递归互斥锁，则在尝试递归锁定互斥锁时，此函数将始终返回false。

- `bool try_lock_until(std::chrono::time_point<Clock, Duration> timePoint)`

  尝试锁定互斥锁。 如果获得了锁，则此函数返回true；否则，返回false。 如果另一个线程已锁定互斥锁，则此功能将至少等待timepoint直到互斥锁可用。
  注意：传递已经传递的timePoint等效于调用try_lock（）。 此行为不同于tryLock（）。
  如果获得了锁定，则互斥锁必须在另一个线程成功锁定之前使用unlock（）进行解锁。
  如果此互斥锁是递归互斥锁，则允许在同一线程的同一互斥锁上多次调用此函数。 如果此互斥锁是非递归互斥锁，则在尝试递归锁定互斥锁时，此函数将始终返回false。

- `void unlock()`

  解锁互斥锁。 尝试用与锁定互斥锁不同的线程解锁互斥锁会导致错误。 解锁未锁定的互斥锁会导致未定义的行为。