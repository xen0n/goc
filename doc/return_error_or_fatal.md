# 返回 error 还是原地 fatal

哪种好呢？在一个纯命令行应用中，及时 fatal，并能在 Panic 中打印出堆栈对调试即为有意。

若是返回 error，虽然看起来：

1. 对每种异常处理都定义的很清楚（有明确的错误消息）
2. 写单测也更容易

但是 Go 的错误处理，导致 error 被一层层返回，以至于在最上层拿到 error 时你都分不清有几层了 -_-，虽然 Go 1.13 的 error wrap 一定程度消减了这个问题，但还是不如 Panic 来的好调试。

而且 goc 并不是一个供大家使用的库，目前来看 fatal 还是更适合。