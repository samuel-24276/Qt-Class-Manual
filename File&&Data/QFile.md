# QFile

继承关系：`QFile`->`QIODevice`->`QObject`

## 1.Public Types



## 2.Public Functions

- qint64 QIODevice::readLine ( char * data, qint64 maxSize )

  此函数从设备读取一行ASCII字符（最大maxSize-1个字节），将字符存储在数据中，并返回读取的字节数。 如果无法读取一行但没有发生错误，则此函数返回0。如果发生错误，则此函数返回可以读取的长度，如果未读取则返回-1。

  始终在数据后附加一个终止的'\ 0'字节，因此maxSize必须大于1。

  读取数据，直到满足以下任一条件：

  - 读取第一个'\ n'字符。
  - maxSize-读取1个字节。
  - 检测到设备数据的结尾。

