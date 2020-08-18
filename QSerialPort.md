# QSerialPort

# 1.Member Type Documentation



## 1.1.enum QSerialPort::BaudRate

该枚举描述了通信设备使用的波特率。

注意：此枚举中仅列出最常见的标准波特率。

| Constant                   | Value  | Description                                                  |
| -------------------------- | ------ | ------------------------------------------------------------ |
| `QSerialPort::Baud1200`    | 1200   | 1200 baud.                                                   |
| `QSerialPort::Baud2400`    | 2400   | 2400 baud.                                                   |
| ` QSerialPort::Baud4800`   | 4800   | 4800 baud.                                                   |
| `QSerialPort::Baud9600`    | 9600   | 9600 baud.                                                   |
| `QSerialPort::Baud19200`   | 19200  | 19200 baud.                                                  |
| ` QSerialPort::Baud38400`  | 38400  | 38400 baud.                                                  |
| `QSerialPort::Baud57600`   | 57600  | 57600 baud.                                                  |
| `QSerialPort::Baud115200`  | 115200 | 115200 baud.                                                 |
| `QSerialPort::UnknownBaud` | -1     | 未知的波特率。 此value已过时。 提供它是为了使旧的源代码正常工作。 我们强烈建议不要在新代码中使用它。 |



## 1.2.enum QSerialPort::DataBits

该枚举描述了所使用的数据位数。

| Constant                       | Value | Description                                                  |
| ------------------------------ | ----- | ------------------------------------------------------------ |
| ` QSerialPort::Data5`          | 5     | 每个字符中的数据位数为5。用于Baudot码。 通常，只有在电传打印机等较旧的设备上才有意义。 |
| `QSerialPort::Data6`           | 6     | 每个字符中的数据位数为6。很少使用。                          |
| `QSerialPort::Data7`           | 7     | 每个字符中的数据位数为7。用于真正的ASCII。 通常，只有在电传打印机等较旧的设备上才有意义。 |
| `QSerialPort::Data8`           | 8     | 每个字符中的数据位数为8。它用于大多数类型的数据，因为此大小与字节的大小匹配。 它几乎在更新的应用程序中普遍使用。 |
| `QSerialPort::UnknownDataBits` | -1    | 位数未知。 此value已过时。 提供它是为了使旧的源代码正常工作。 我们强烈建议不要在新代码中使用它。 |



## 1.3.enum QSerialPort::Direction 或flags QSerialPort::Directions

该枚举描述了数据传输的可能方向。
注意：此枚举用于在某些操作系统（例如POSIX之类）上针对每个方向分别设置设备的波特率。

| Constant                         | Value  | Description                       |
| -------------------------------- | ------ | --------------------------------- |
| `QSerialPort::Input`             | 1      | Input direction.                  |
| `QSerialPort::Output`            | 2      | Output direction.                 |
| `QSerialPort::AllDirectionsInput | Output | Simultaneously in two directions. |



## 1.4.enum QSerialPort::FlowControl

该枚举描述了使用的流量控制。

| Constant                          | Value | Description                                                  |
| --------------------------------- | ----- | ------------------------------------------------------------ |
| `QSerialPort::NoFlowControl`      | 0     | No flow control.                                             |
| `QSerialPort::HardwareControl`    | 1     | Hardware flow control (RTS/CTS).                             |
| `QSerialPort::SoftwareControl`    | 2     | Software flow control (XON/XOFF).                            |
| `QSerialPort::UnknownFlowControl` | -1    | 未知的流量控制。 此value已过时。 提供它是为了使旧的源代码正常工作。 我们强烈建议不要在新代码中使用它。 |



## 1.5.enum QSerialPort::Parity

| Constant                     | Value | Description                                                  |
| ---------------------------- | ----- | ------------------------------------------------------------ |
| `QSerialPort::NoParity`      | 0     | 它没有发送奇偶校验位。 这是最常见的奇偶校验设置。 错误检测由通信协议处理 |
| `QSerialPort::EvenParity`    | 2     | 每个字符中1位的数量（包括奇偶校验位）始终为偶数。            |
| `QSerialPort::OddParity`     | 3     | 每个字符（包括奇偶校验位）中1位的数目始终为奇数。 它确保每个字符中至少发生一个状态转换。 |
| `QSerialPort::SpaceParity`   | 4     | 空间奇偶。 在空间信号条件下发送奇偶校验位。 它不提供错误检测信息。 |
| `QSerialPort::MarkParity`    | 5     | 标记奇偶。 奇偶校验位始终设置为标记信号条件（逻辑1）。 它不提供错误检测信息。 |
| `QSerialPort::UnknownParity` | -1    | 未知的奇偶校验。 此value已过时。 提供它是为了使旧的源代码正常工作。 我们强烈建议不要在新代码中使用它。 |



## 1.6.enum QSerialPort::StopBits

该枚举描述了所使用的停止位的数量。

| Constant                       | Value | Description                                                  |
| ------------------------------ | ----- | ------------------------------------------------------------ |
| `QSerialPort::OneStop`         | 1     | 1 stop bit.                                                  |
| `QSerialPort::OneAndHalfStop`  | 3     | 1.5个停止位。 这仅适用于Windows平台。                        |
| `QSerialPort::TwoStop`         | 2     | 2 stop bit.                                                  |
| `QSerialPort::UnknownStopBits` | -1    | 停止位数未知。 此value已过时。 提供它是为了使旧的源代码正常工作。 我们强烈建议不要在新代码中使用它。 |

# 2.Detailed Description

您可以使用`QSerialPortInfo`帮助程序类获取有关可用串行端口的信息，该类允许枚举系统中的所有串行端口。这对于获取要使用的串行端口的正确名称很有用。您可以将帮助程序类的对象作为参数传递给`setPort（）`或`setPortName（）`方法，以分配所需的串行设备。
设置端口后，可以使用`open（）`方法以只读（r / o），仅写（w / o）或读写（r / w）模式打开它。

注意：**串行端口始终以独占访问方式打开**（也就是说，没有其他进程或线程可以访问已打开的串行端口）。
使用close（）方法关闭端口并取消I / O操作。
成功打开后，QSerialPort会尝试确定端口的当前配置并对其进行初始化。您可以使用setBaudRate（），setDataBits（），setParity（），setStopBits（）和setFlowControl（）方法将端口重新配置为所需的设置。

有两个属性可与**引出信号**(pinout signals)配合使用，即：`QSerialPort :: dataTerminalReady`，`QSerialPort :: requestToSend`。 也可以使用`pinoutSignals（）`方法查询当前的引脚分配信号集。
一旦知道端口已准备好读取或写入，就可以使用read（）或write（）方法。 另外，还可以调用readLine（）和readAll（）便捷方法。 如果不是一次读取所有数据，则剩余的数据将在以后提供，因为新的传入数据将附加到QSerialPort的内部读取缓冲区中。 您可以使用`setReadBufferSize（）`限制读取缓冲区的大小。
QSerialPort提供了一组函数，这些函数可以**挂起调用线程，直到发出某些信号为止**。 这些功能可用于**实现阻塞串行端口**：

- `waitForReadyRead() `阻止调用，直到可以**读取**新数据为止。
- `waitForBytesWritten()` 阻止调用，直到将一个有效载荷数据**写入**串行端口为止。

See the following example:

```c++
 int numRead = 0, numReadTotal = 0;
 char buffer[50];

 for (;;) {
     numRead  = serial.read(buffer, 50);

     // Do whatever with the array

     numReadTotal += numRead;
     if (numRead == 0 && !serial.waitForReadyRead())
         break;
 }
```

如果waitForReadyRead（）返回false，则说明连接已关闭或发生了错误。
如果在任何时间点发生错误，QSerialPort将发出`errorOccurred（）`信号。 您也可以调用error（）来查找最后发生的错误的类型。

**注意**：并非所有错误条件都是在QSerialport中以平台独立的方式处理的，例如，成帧，奇偶校验和中断条件错误。这些类型的错误需要由应用程序代码处理，可能使用设备描述符上的OS系统特定的ioctl、和/或解析流的字节填充。
使用阻塞串行端口进行编程与使用非阻塞串行端口进行编程完全不同。**阻塞的串行端口不需要事件循环，通常可以简化代码**。但是，**在GUI应用程序中，阻塞串行端口应仅在非GUI线程中使用，以避免冻结用户界面**。
QSerialPort类也可以与QTextStream和QDataStream的流运算符（operator <<（）和operator >>（））一起使用。但是，有一个问题需要注意：在尝试使用operator >>（）重载运算符进行读取之前，请确保有足够的数据可用。

# 3.Properties



| 属性名            | 属性类型        |
| ----------------- | --------------- |
| baudRate          | qint32          |
| flowControl       | FlowControl     |
| breakEnabled      | bool            |
| parity            | Parity          |
| dataBits          | DataBits        |
| requestToSend     | bool            |
| dataTerminalReady | bool            |
| stopBits          | StopBits        |
| error             | SerialPortError |

# 4.Public Functions

- `QSerialPort(const QSerialPortInfo &serialPortInfo, QObject *parent = nullptr)`

  `QSerialPort(const QString &name, QObject *parent = nullptr)`

  `QSerialPort(QObject *parent = nullptr)`

- `virtual ~QSerialPort()`

- `qint32 baudRate(QSerialPort::Directions directions = AllDirections) const`

  此属性保存所需方向directions 的数据波特率
  如果设置成功或在打开端口之前进行设置，则返回true；否则返回false并设置一个错误代码，该错误代码可以通过访问`QSerialPort :: error`属性的值来获取。要设置波特率，请使用枚举`QSerialPort :: BaudRate`或任何正的qint32值。
  注意：**如果在打开端口之前设置了该设置，则在成功打开端口之后，将在QSerialPort :: open（）方法中自动完成实际的串行端口设置**。
  警告：在所有平台上都支持设置AllDirections标志。 Windows仅支持此模式。
  警告：在Windows的任何方向上返回相等的波特率。
  缺省值为Baud9600，即每秒9600位。

  Access functions(访问功能的函数)

  - `qint32 baudRate()`

  - `bool setBaudRate(`)

  相关信号：`void baudRateChanged()`

- `bool clear(QSerialPort::Directions directions = AllDirections)`

  根据给定的方向，丢弃输出或输入缓冲区中的所有字符。 这包括清除内部类缓冲区和UART（驱动程序）缓冲区。 同时终止挂起的读取或写入操作。 如果成功，则返回true； 否则返回false。
  注意：在尝试清除任何缓冲的数据之前，必须先打开串行端口；否则返回false并设置NotOpenError错误代码。

- `void clearError()`

  此属性保存串行端口的错误状态
  I / O设备状态返回错误代码。 例如，如果open（）返回false，或者读/写操作返回-1，则此属性可用于确定操作失败的原因。
  调用clearError（）后，错误代码设置为默认的QSerialPort :: NoError。

- `QSerialPort::DataBits dataBits() const`

  此属性将数据位保存在一个帧中
  如果设置成功或在打开端口之前进行设置，则返回true；否则返回false并设置一个错误代码，该错误代码可以通过访问QSerialPort :: error属性的值来获取。
  注意：如果在打开端口之前设置了该设置，则在成功打开端口之后，将在QSerialPort :: open（）方法中自动完成实际的串行端口设置。
  缺省值为Data8，即8个数据位。

  Access functions(访问功能的函数)

  - `QSerialPort::DataBits dataBits() const`
  - `bool setDataBits(QSerialPort::DataBits dataBits)`

  相关信号：`void dataBitsChanged(QSerialPort::DataBits dataBits)`

- `QSerialPort::SerialPortError error() const`

- `QSerialPort::FlowControl flowControl() const`

  此属性保持所需的流量控制模式
  如果设置成功或在打开端口之前进行设置，则返回true； 否则返回false并设置一个错误代码，该错误代码可以通过访问QSerialPort :: error属性的值来获取。
  注意：如果在打开端口之前设置了该设置，则在成功打开端口之后，将在QSerialPort :: open（）方法中自动完成实际的串行端口设置。
  默认值为NoFlowControl，即无流控制。

  Access functions(访问功能的函数)

  - `QSerialPort::FlowControl flowControl() const`
  - `bool setFlowControl(QSerialPort::FlowControl flowControl)`

  相关信号：`void flowControlChanged(QSerialPort::FlowControl flow)`

- `bool flush()`

  此函数尽可能不阻塞地将内部写入缓冲区的数据写入基础串行端口。 如果写入了任何数据，则此函数返回true；否则返回false。
  调用此函数可将缓冲的数据立即发送到串行端口。 成功写入的字节数取决于操作系统。 在大多数情况下，不需要调用此函数，因为一旦控制权返回事件循环，QSerialPort类将自动开始发送数据。 如果没有事件循环，请改为调用`waitForBytesWritten（）`。
  注意：在尝试刷新任何缓冲的数据之前，必须先打开串行端口； 否则返回false并设置NotOpenError错误代码。

- `QSerialPort::Handle handle() const`

- `bool isBreakEnabled() const`

- `bool isDataTerminalReady()`

- `bool isRequestToSend()`

  此属性保留线路信号RTS的状态（高或低）
  成功返回true，否则返回false。 如果该标志为真，则将RTS信号设置为高； 否则低。
  注意：在尝试设置或获取此属性之前，必须先打开串行端口。 否则，返回false并将错误代码设置为NotOpenError。
  注意：在HardwareControl模式下尝试控制RTS信号的尝试将失败，错误代码设置为UnsupportedOperationError，因为该信号由驱动程序自动控制。

  Access functions(访问功能的函数):

  | bool | isRequestToSend()            |
  | ---- | ---------------------------- |
  | bool | setRequestToSend(bool *set*) |

  相关信号：`void requestToSendChanged(bool set)`

- `QSerialPort::Parity parity() const`

- `QSerialPort::PinoutSignals pinoutSignals()`

- `QString portName() const`

- `qint64 readBufferSize() const`

- `bool sendBreak(int duration = 0)`

- `bool setBaudRate(qint32 baudRate, QSerialPort::Directions directions = AllDirections)`

- `bool setBreakEnabled(bool set = true)`

- `bool setDataBits(QSerialPort::DataBits dataBits)`

- `bool setDataTerminalReady(bool set)`

- `bool setFlowControl(QSerialPort::FlowControl flowControl) `

- `bool setParity(QSerialPort::Parity parity)`

- `void setPort(const QSerialPortInfo &serialPortInfo)`

- `void setPortName(const QString &name)`

- `void setReadBufferSize(qint64 size)`

- `bool setRequestToSend(bool set)`

- `bool setStopBits(QSerialPort::StopBits stopBits)`

- `QSerialPort::StopBits stopBits() const`

# 5.Reimplemented Public Functions

- `virtual bool atEnd() const override`
- `virtual qint64 bytesAvailable() const override`
- `virtual qint64 bytesToWrite() const override`
- `virtual bool canReadLine() const override`
- `virtual void close() override`
- `virtual bool isSequential() const override`
- `virtual bool open(QIODevice::OpenMode mode) override`
- `virtual bool waitForBytesWritten(int msecs = 30000) override`
- `virtual bool waitForReadyRead(int msecs = 30000) override`

# 6.Signals

- `void baudRateChanged(qint32 baudRate, QSerialPort::Directions directions)`
- `void breakEnabledChanged(bool set)`
- `void dataBitsChanged(QSerialPort::DataBits dataBits)`
- `void dataTerminalReadyChanged(bool set)`
- `void errorOccurred(QSerialPort::SerialPortError error)`
- `void flowControlChanged(QSerialPort::FlowControl flow)`
- `void parityChanged(QSerialPort::Parity parity)`
- `void requestToSendChanged(bool set)`
- `void stopBitsChanged(QSerialPort::StopBits stopBits)`

# 7.Reimplemented Protected Functions

- `virtual qint64 readData(char *data, qint64 maxSize) override`
- `virtual qint64 readLineData(char *data, qint64 maxSize) override`
- `virtual qint64 writeData(const char *data, qint64 maxSize) override`