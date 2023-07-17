# syncmap
sync.Map 是 Go 语言标准库中的一个并发安全的键值对集合, 用于在并发环境下进行读取和写入操作。
自官方在 1.9 加入了 sync.Map 之后, 就一直没有获取键值对数量的方法, 导致每次都需要调用 Range 方法来统计, 为了解决这个简单而又繁琐的问题, 基于 Go1.20 对 sync.Map 新增了 Len 方法, 用于获取 sync.Map 中存储的键值对个数。

# 原理
在 sync.Map 类型中增加了一个 int64 类型的属性 size, 分别在 Swap、LoadOrStore、LoadAndDelete、CompareAndDelete、dirtyLocked方法中新增了对 size 属性的处理逻辑。
