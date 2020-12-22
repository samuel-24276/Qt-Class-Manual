# tr()方法使用

返回源文本的翻译版本，可以选择基于歧义消除字符串和包含复数的字符串的n值； 否则，如果没有合适的翻译字符串，则返回sourceText本身。

```c++
void MainWindow::createMenus()
{
    fileMenu = menuBar()->addMenu(tr("&File"));
    ...
    // 菜单栏，工具栏，Action文字的&符号，表示&符号后面的字母是触发的快捷键
    // 菜单栏无法被&符号后的字母触发
}
```

