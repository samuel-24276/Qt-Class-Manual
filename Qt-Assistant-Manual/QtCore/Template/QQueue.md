# QQueue

继承关系：`QQueue`->`QList`

## 1.Public Functions

- T dequeue()

  删除队列中的标题项并返回它。 此函数假定队列不为空。
  这与QList :: takeFirst（）相同。

- void enqueue(const T &t)

  将值t添加到队列的尾部。
  这与QList :: append（）相同。

- T &head()

  返回对队列标题的引用。 此函数假定队列不为空。
  这与QList :: first（）相同。

- const T &head() const

  重载函数

- void swap(QQueue<T> &other)

  使用此队列交换其他队列。 此操作非常快，并且永远不会失败。

## 2.Detailed Description

QQueue <T>是Qt的通用容器类之一。 它为相同类型的项目实现队列数据结构。
队列是先进先出（FIFO）结构。 使用enqueue（）将项目添加到队列的末尾，并使用dequeue（）从项目头检索项目。 head（）函数提供对标题项的访问，而无需删除它。

QQueue从QList继承。 **QList的所有功能也适用于QQueue**。 例如，可以使用isEmpty（）测试队列是否为空，并且可以使用QList的迭代器类（例如QListIterator）遍历QQueue。 此外，QQueue提供了三个便利函数，可轻松实现FIFO语义：enqueue（），dequeue（）和head（）。
QQueue的值类型必须是可分配的数据类型。 这涵盖了大多数常用的数据类型，但是**编译器不允许您例如将QWidget存储为值。 请改用QWidget ***。