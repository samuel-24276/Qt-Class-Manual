# QStack

继承关系：`QStack`->`QVector`

## 1.Public Functions

- T pop()

  从栈中删除顶层项目并返回。 此函数假定栈不为空。

- void push(const T &t)

  将元素t添加到栈的顶部。
  这与QVector :: append（）相同。

- void swap(QStack<T> &other)

  将此栈与其他栈交换数据。 此操作非常快，并且永远不会失败。

- T &top()

  返回对栈顶部项目的引用。 该函数假定栈不为空。
  这与QVector :: last（）相同。

- const T &top() const

  重载函数

## 2.Detailed Description

QStack <T>是Qt的通用容器类之一。 它为相同类型的项目实现栈数据结构。
栈是后进先出（LIFO）结构。 使用push（）将项目添加到栈的顶部，并使用pop（）从顶部检索项目。 top（）函数提供对最顶层项目的访问，而无需删除它。

QStack继承自QVector。 **QVector的所有功能也适用于QStack**。 例如，可以使用isEmpty（）测试栈是否为空，并且可以使用QVector的迭代器类（例如QVectorIterator）遍历QStack。 此外，QStack提供了三个便利的功能，可轻松实现LIFO语义：push（），pop（）和top（）。
QStack的值类型必须是可分配的数据类型。 这涵盖了大多数常用的数据类型，但是**编译器不允许您将QWidget存储为值。 而是存储一个QWidget ***。