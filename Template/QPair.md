# QPair

## 1.Public Types

- typedef first_type
- typedef second_type

## 2.Public Functions

- QPair(QPair<TT1, TT2> &&p)
- QPair(const QPair<TT1, TT2> &p)
- QPair(const T1 &value1, const T2 &value2)
- QPair()
- void swap(QPair<T1, T2> &other)
- QPair<T1, T2> &operator=(const QPair<TT1, TT2> &p)
- QPair<T1, T2> &operator=(QPair<TT1, TT2> &&p)

## 3.Public Variables

- T1 first
- T2 second

## 4.Related Non-Members

- QPair<T1, T2> qMakePair(const T1 &value1, const T2 &value2)
- void swap(QPair<T1, T2> &lhs, QPair<T1, T2> &rhs)
- bool operator!=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- bool operator<(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- QDataStream &operator<<(QDataStream &out, const QPair<T1, T2> &pair)
- bool operator<=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- bool operator==(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- bool operator>(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- bool operator>=(const QPair<T1, T2> &p1, const QPair<T1, T2> &p2)
- QDataStream &operator>>(QDataStream &in, QPair<T1, T2> &pair)

## 5.Detailed Description

