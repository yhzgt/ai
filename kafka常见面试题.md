# kafka常见面试题

## kafka重复消费的场景

1. 在Consumer消费的过程中，应用程序被强制kill掉或者宕机，可能会导致Offset没提交，从而产生重复提交的问题。
2. 在Kafka里面有一个Partition Balance机制，就是把多个Partition均衡的分配给多个消费者。Consumer端会从分配的Partition里面去消费消息，如果一个consumer的消费超过max.poll.interval.ms的设置时间或者默认的5分钟，将会触发Partition Balance机制，导致数据重复。
   解决方案：可以将max.poll.interval.ms保持默认时间或者可以根据业务设置长一些。
3. 

# 延迟消息的五种实现方案

## kafka的topic的清除策略



## 关于自动提交的问题

1. 自动提交

   1. 当发生异常的时候是否会自动提交
      不会

   2. 当auto-commit-interval=1000时，但是程序1s没有执行完成也没有报错，后面在3s时候报错了，是否会造成消息丢失？

      不会，因为Spring会检查程序是否还在运行。

2. 手动提交

   1. 当无异常的时候是否会自动提交
      会自动提交。