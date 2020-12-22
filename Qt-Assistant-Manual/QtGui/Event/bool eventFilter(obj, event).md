# `bool eventFilter(QObject *obj, QEvent *event);`事件过滤器

- 事件过滤器可以对其他控件接收到的事件进行监控
- 任意的QObject对象都可以作为事件过滤器使用
- 事件过滤器对象需要重启eventFilter() 函数
- 组件通过installEventFilter() 函数安装事件过滤器
- 事件过滤器**在控件之前接收到事件**
- 事件过滤器能够决定是否将事件转发到控件对象

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190716101502276.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190716101511557.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NtYWxsX3ByaW5jZV8=,size_16,color_FFFFFF,t_70)



示例：

```c++
bool FourBaseDialog::eventFilter(QObject *obj, QEvent *event)       
// 事件过滤，由编辑框的视口viewport安装，
{
    if (obj == ui->ContentTE->viewport())
    {
        if (event->type() == QEvent::MouseButtonPress)//
        {
            QMouseEvent *mouseevent = dynamic_cast<QMouseEvent *>(event);
            if (mouseevent->buttons() == Qt::LeftButton)
            {
                QDesktopServices::openUrl(QUrl(ui->ContentTE->toPlainText()));
                return true;
            }
            return false;
        }
        else    // 若event->type()不是对应事件的类型，则返回false
        {
            return false;
        }
    }
    else        // 若obj不是对应控件对象，则把事件传至父窗口
    {
        return QDialog::eventFilter(obj, event);
    }
}
```

控件的事件过滤器由其自身的视口（viewport）安装，installEventFilter()参数为视口的父控件即该控件本身。在不需要重写该控件时使用事件过滤器十分方便，一旦重写该控件，则重写事件过滤器里的相关事件的Event效率更高。











