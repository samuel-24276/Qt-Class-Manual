# QByteArray

> QString 转  QByteArray通过toUtf8()方法，反之可以直接转。

# 1.Detailed Description

QByteArray可用于存储原始字节（包括'\ 0'）和传统的8位'\ 0'终止的字符串。 **使用QByteArray比使用const char *更方便**。 在幕后，它始终确保数据后面带有“ \ 0”终止符，并使用**隐式共享（写时复制）**来减少内存使用量并避免不必要的数据复制。

除了QByteArray，Qt还提供了QString类来存储字符串数据。 对于大多数目的，**QString**是您要使用的类。 它**存储16位Unicode字符，使在应用程序中轻松存储非ASCII /非Latin1字符成为可能**。 此外，在Qt API中始终使用QString。 ***QByteArray适用的两种主要情况是：您需要存储原始二进制数据时，以及内存保护至关重要时***（例如，使用Qt for Embedded Linux）。

初始化QByteArray的一种方法就是将const char *传递给其构造函数。 例如，以下代码创建一个大小为5的字节数组，其中包含数据“ Hello”：

```c++
QByteArray ba（“ Hello”）;
```

尽管size（）为5，但字节数组在末尾还保留了一个额外的'\ 0'字符，因此，如果使用的函数要求指向基础数据的指针（例如，对data（）的调用）， 指向的数据保证以'\ 0'结尾。
QByteArray会复制const char *数据的深层副本，因此您以后可以修改它而不会出现副作用。 （如果出于性能原因，**您不想获取字符数据的深层副本，请改用QByteArray :: fromRawData（）**。）
另一种方法是使用resize（）设置数组的大小并初始化每个字节的数据字节。 QByteArray使用基于0的索引，就像C ++数组一样。 要访问特定索引位置的字节，可以使用operator []（）。 **在非常量字节数组上，operator []（）返回对可在赋值左侧使用的字节的引用**。 例如：

```c++
QByteArray ba;
ba.resize(5);
ba[0] = 0x3c;
ba[1] = 0xb8;
ba[2] = 0x64;
ba[3] = 0x18;
ba[4] = 0xca;
```

对于只读访问，另一种语法是使用at（）：

```c++
for（int i = 0; i <ba.size（）; ++ i）{
      if（ba.at（i）> ='a'&& ba.at（i）<='f'）
          cout <<“Found character in range [a-f]” << Qt :: endl;
}
```

**at（）可以比operator []（）更快，因为它永远不会导致深度复制的发生**。
要一次提取多个字节，请使用left（），right（）或mid（）。
**QByteArray可以嵌入“ \ 0”字节**。 size（）函数始终返回整个数组的大小，包括嵌入的'\ 0'字节，但不包括QByteArray添加的终止符'\ 0'。 例如：

```c++
 QByteArray ba1("ca\0r\0t");	//不指定大小，则以\0结尾
 ba1.size();                     // Returns 2.
 ba1.constData();                // Returns "ca" with terminating \0.

 QByteArray ba2("ca\0r\0t", 3);  //指定大小，\0会被读取，但末尾还是\0
 ba2.size();                     // Returns 3.
 ba2.constData();                // Returns "ca\0" with terminating \0.

 QByteArray ba3("ca\0r\0t", 4);
 ba3.size();                     // Returns 4.
 ba3.constData();                // Returns "ca\0r" with terminating \0.

 const char cart[] = {'c', 'a', '\0', 'r', '\0', 't'};
 QByteArray ba4(QByteArray::fromRawData(cart, 6));
 ba4.size();                     // Returns 6.
 ba4.constData();                // Returns "ca\0r\0t" without terminating \0.

```

- **如果要获取直到第一个'\ 0'字符为止的数据长度，请在字节数组上调用`qstrlen（)`**。
- 调用`resize（）`之后，新分配的字节具有未定义的值。 要将所有字节设置为特定值，请调用`fill（）`。
- 要获得指向实际字符数据的指针，请调用data（）或constData（）。 这些函数返回一个指向数据开头的指针。 保证指针保持有效，直到在QByteArray上调用非常量函数为止。 除非从原始数据创建了QByteArray，否则还可以保证数据以“ \ 0”字节结尾。 此'\ 0'字节由QByteArray自动提供，不计入size（）中。
  QByteArray提供以下用于修改字节数据的基本功能：append（），prepend（），insert（），replace（）和remove（）。 例如：

```c++
 QByteArray x("and");
 x.prepend("rock ");         // x == "rock and"
 x.append(" roll");          // x == "rock and roll"
 x.replace(5, 3, "&");       // x == "rock & roll"
```

`replace（）`和`remove（）`函数的前两个参数是开始擦除的位置以及应擦除的字节数。

- **当将`append（）`数据追加到非空数组时，将重新分配该数组并将新数据复制到该数组。您可以通过调用reserve（）来避免此行为，该方法会预先分配一定数量的内存**。您也可以调用Capacity（）来找出QByteArray实际分配了多少内存。追加到空数组的数据不会被复制。
  常见的要求是从字节数组中删除空格字符（'\ n'，'\ t'，''等）。

- **如果要从QByteArray的两端删除空格，请使用`trimmed（）`**。

- **如果要从两端删除空格，并用字节数组中的单个空格字符替换多个连续的空格，请使用`simpleed（）`**。
- **如果要查找QByteArray中所有出现的特定字符或子字符串，请使用`indexOf（）`或`lastIndexOf（）`**。前者从给定的索引位置开始向前搜索，后者向后搜索。两者都返回字符或子字符串的索引位置（如果找到）；否则，它们返回-1。例如，这是一个典型的循环，查找所有出现的特定子字符串：

```c++
 QByteArray ba("We must be <b>bold</b>, very <b>bold</b>");
 int j = 0;
 while ((j = ba.indexOf("<b>", j)) != -1) {
     cout << "Found <b> tag at index position " << j << Qt::endl;
     ++j;
 }
```

- **如果只想检查QByteArray是否包含特定字符或子字符串，请使用contains（）**。

- **如果要确定某个特定字符或子字符串在字节数组中出现多少次，请使用count（）**。

- **如果要用另一个替换所有出现的特定值，请使用两个参数的replace（）重载之一**。
  可以使用重载运算符（例如operator <（），operator <=（），operator ==（），operator> =（）等）来比较QByteArrays。这种比较仅基于字符的数值，并且非常快，但不是人们期望的。 **QString :: localeAwareCompare（）是对用户界面字符串进行排序的更好选择**。
  由于历史原因，QByteArray区分`null byte array`和`empty byte array`。`null byte array`是使用QByteArray的默认构造函数或通过将（const char *）0传递给构造函数初始化的字节数组。`empty byte array`是任何大小为0的字节数组。`null byte array`始终为空，但`empty byte array`不一定为null：

  ```c++
   QByteArray().isNull();          // returns true
   QByteArray().isEmpty();         // returns true
  
   QByteArray("").isNull();        // returns false
   QByteArray("").isEmpty();       // returns true
  
   QByteArray("abc").isNull();     // returns false
   QByteArray("abc").isEmpty();    // returns false
  ```

  除isNull（）外的所有函数都将`null byte array`与`empty byte array`视为相同。 例如，data（）返回一个有效的指针（不是nullptr）指向字节数组的'\ 0'字符，并且QByteArray（）比较等于QByteArray（“”）。 **我们建议您始终使用isEmpty（）并避免使用isNull（）。**

# 2.Maximum size and out-of-memory conditions

当前版本的QByteArray的大小限制在2 GB（2 ^ 31字节）以下。 确切的值取决于体系结构，因为**它取决于管理数据块所需的开销，但不超过32个字节**。 原始数据块还受当前版本中使用int类型限制为2 GB减去1个字节。
万一内存分配失败，QByteArray将抛出std :: bad_alloc异常。 Qt容器中的内存不足情况是Qt引发异常的唯一情况。
请注意，操作系统可能会对拥有大量分配的内存（尤其是大的连续块）的应用程序施加进一步的限制。 这些注意事项，此类行为的配置或任何缓解措施均不在QByteArray API的范围之内。

# 3.Number-String Conversions

在C语言环境中执行在数字数据类型和字符串之间执行转换的函数，与用户的语言环境设置无关。 使用QString在数字和字符串之间执行可感知区域设置的转换。
8位字符比较
在QByteArray中，在Latin-1语言环境中完成了大写和小写以及字符大于或小于另一个字符的概念。 这会影响参数比较或区分大小写不敏感的函数。 如果两个字符串都只包含Latin-1字符，则不区分大小写的操作和比较将是准确的。 影响的函数包括contains（），indexOf（），lastIndexOf（），operator <（），operator <=（），operator>（），operator> =（），isLower（），isUpper（），toLower（） 和toUpper（）。
此问题不适用于QString，因为它们使用Unicode表示字符。

# 4.Member Type Documentation

# 5.Member Function Documentation

