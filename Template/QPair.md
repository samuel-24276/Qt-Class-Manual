# QPair

## 1.Public Types

- typedef first_type

  The type of the first element in the pair (T1)

- typedef second_type

  The type of the second element in the pair (T2).

## 2.Public Functions

- `QPair(QPair<T1, T2> &&p)`
- `QPair(const QPair<T1, T2> &p)`
- `QPair(const T1 &value1, const T2 &value2)`
- `QPair()`
- `void swap(QPair<T1, T2> &other)`
- `QPair<T1, T2> &operator=(const QPair<TT1, TT2> &p)`
- `QPair<T1, T2> &operator=(QPair<TT1, TT2> &&p)`

## 3.Public Variables

- `T1 first`
- `T2 second`

## 4.Related Non-Members

- **`QPair<T1, T2> qMakePair(const T1 &value1, const T2 &value2)`**

  返回包含值1和值2的QPair <T1，T2>。 

- void swap(QPair<T1, T2> &lhs, QPair<T1, T2> &rhs)

- bool operator!=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- bool operator<(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- **QDataStream &operator<<(QDataStream &out, const QPair<T1, T2> &pair)**

  写成Pair输出。
  此函数需要T1和T2类型来实现operator <<（）。

- bool operator<=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- bool operator==(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- bool operator>(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- bool operator>=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)

- **QDataStream &operator>>(QDataStream &in, QPair<T1, T2> &pair)**

  从流中读取一对Pair。
  此函数需要T1和T2类型来实现operator <<（）。

## 5.Detailed Description

如果STL对类型不可用，则可以在您的应用程序中使用QPair <T1，T2>。 它存储一个T1类型的值和一个T2类型的值。 它可以用作需要返回两个值的函数的返回值，也可以用作通用容器的值类型。

**C ++ 11自动变量类型推导（auto）的出现将重点从类型名称转移到函数和成员的名称**。 因此，像std :: pair和std :: tuple一样，QPair在无法定义专用类型的通用（模板）代码中最有用。

QPair的模板数据类型（T1和T2）必须是可分配的数据类型。 例如，您不能将QWidget存储为值。 而是存储一个QWidget *。 一些功能有其他要求； 这些要求是按功能记录的。