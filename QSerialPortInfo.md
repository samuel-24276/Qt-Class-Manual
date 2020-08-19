# QSerialPortInfo

# 0.读取串口数据的步骤

> 1.利用串口信息类来设置串口`setPort(QSerialPortInfo info)`
>
> 2.打开串口open()，打开方式是`QIODevice`的几种读写方式
>
> 3.获取串口名字`portName()`并显示在comboBox上，之后关闭串口`close()`
>
> 4.利用comboBox的内容初始化端口

## 0.1.找到机器上的串口

```c++
void Widget::find_serialport()
{
    //查找可用的串口
    foreach(const QSerialPortInfo &info, QSerialPortInfo::availablePorts())
    {
        QSerialPort serial;
        serial.setPort(info);   //设置串口
        if(serial.open(QIODevice::ReadWrite))
        {
            ui->com->addItem(serial.portName());        //界面的comboBox显示串口name
            serial.close();
        }
    }
}
```

## 0.2.打开串口并监听串口信号readyRead()

```c++
void Widget::on_open_serialport_clicked()//界面上打开串口按钮的槽函数
{
    find_serialport();

    if(ui->com->count() != 0)   //不为空时
        //初始化串口
            serialport->setPortName(ui->com->currentText());        //设置串口名
            if(serialport->open(QIODevice::ReadWrite))              //打开串口成功
            {
               serialport->setBaudRate(9600);       //设置波特率
               serialport->setDataBits(QSerialPort::Data8);
               serialport->setParity(QSerialPort::NoParity);
               serialport->setStopBits(QSerialPort::OneStop);
               serialport->setStopBits(QSerialPort::TwoStop);
               serialport->setFlowControl(QSerialPort::NoFlowControl);     //设置流控制
               QObject::connect(serialport, &QSerialPort::readyRead, this, &Widget::read_serialport);    //读数据
                //控件可见设置
               ui->start->setEnabled(true);
               ui->close_serialport->setEnabled(true);
               ui->open_serialport->setEnabled(false);
               ui->label_state->setText(tr("串口打开成功"));
               ui->widget->replot();       //画图
                // 操作记录
               QString current_date = ui->textEdit->toPlainText();
               QDateTime current_date_time =QDateTime::currentDateTime();   //获取当前时间
               current_date +=current_date_time.toString("yyyy.MM.dd hh:mm");
               current_date += " 打开串口" ;
               current_date += "\n";
               ui->textEdit->setText(current_date);
            }
            else    //打开失败提示
            {
                QMessageBox::information(this,tr("Erro"),tr("Open the failure"),QMessageBox::Ok);
                ui->label_state->setText(tr("串口未打开"));
            }
}
```

## 0.3.读取串口数据

```c++
void Widget::read_serialport()
{
    QByteArray buf;
    buf = serialport->readAll();

    if(!buf.isEmpty())          //显示数据
    {
        QString ss = tr(buf);
        temperature = ss.toDouble();
        ui->lcdNumber->display(temperature);    //lcd显示数据
        qDebug()<<buf<<temperature;
    }

    buf.clear();    //清空缓存区
}
```

## 0.4.关闭串口

```c++
void Widget::on_close_serialport_clicked()
{
    //关闭串口
    serialport->clear();        //清空缓存区
    serialport->close();        //关闭串口
    on_pause_clicked();
    ui->start->setEnabled(false);

    // 操作记录
    QString current_date = ui->textEdit->toPlainText();
    QDateTime current_date_time =QDateTime::currentDateTime();   //获取当前时间
    current_date +=current_date_time.toString("yyyy.MM.dd hh:mm");
    current_date += " 关闭串口" ;
    current_date += "\n\n";
    ui->textEdit->setText(current_date);

    //控件设置
    ui->open_serialport->setEnabled(true);
    ui->close_serialport->setEnabled(false);
    ui->label_state->setText(tr("串口 关闭"));

    // lcd 显示 0
    temperature = 00.0;
    ui->lcdNumber->display(temperature);
}
```

# 1.Detailed Description

使用静态函数生成QSerialPortInfo对象的列表。 列表中的每个QSerialPortInfo对象代表一个串行端口，可以查询该端口的名称，系统位置，描述和制造商。 **QSerialPortInfo类也可用作QSerialPort类的setPort（）方法的输入参数。**

# 2.Public Functions

- `QSerialPortInfo(const QSerialPortInfo &other)`
- `QSerialPortInfo(const QString &name)`
- `QSerialPortInfo(const QSerialPort &port)`
- `QSerialPortInfo()`
- `QSerialPortInfo& operator=(const QSerialPortInfo &other)`
- `~QSerialPortInfo()`
- `QString description() const`
- `bool hasProductIdentifier() const`
- `bool hasVendorIdentifier() const`
- `bool isNull() const`
- `QString manufacturer() const`
- `QString portName() const`
- `quint16 productIdentifier() const`
- `QString serialNumber() const`
- `void swap(QSerialPortInfo &other)`
- `QString systemLocation() const`
- `quint16 vendorIdentifier() const`

# 3.Static Public Members

- `QList<QSerialPortInfo> availablePorts()`
- `QList<qint32> standardBaudRates()`

