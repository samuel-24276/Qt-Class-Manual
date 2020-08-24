# QTimer定时器

# 1.Properties

- `active : const bool`

  如果计时器正在运行，则此布尔属性为true；否则为false。 否则为假。

- `interval : int`

  此属性保存超时间隔（以毫秒为单位）
  此属性的默认值为0。超时间隔为0的QTimer将在处理完窗口系统的事件队列中的所有事件后立即超时。
  设置活动计时器的间隔会更改其timerId（）。

- `remainingTime : const int`

  此属性保留剩余时间（以毫秒为单位）
  返回计时器的剩余值（以毫秒为单位），直到超时。 如果计时器处于非活动状态，则返回值为-1。 如果计时器过期，则返回值为0。

- `singleShot : bool`

  此属性保存计时器是否为单次计时器
  单发计时器仅触发一次，非单发计时器每间隔毫秒触发一次。
  此属性的默认值为false。

- `timerType : Qt::TimerType`

  控制计时器的精度
  此属性的默认值为`Qt :: CoarseTimer`。

