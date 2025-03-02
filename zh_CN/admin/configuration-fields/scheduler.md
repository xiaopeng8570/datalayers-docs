# 调度器配置

`scheduler` 部分管理 Datalayers 系统的作业调度，包括 memtable 数据落盘、垃圾回收（GC）和SST Compact等任务。这些设置帮助控制系统在负载下可以并发运行多少作业，以及可以排队多少作业。

## Flush Job配置

`flush` Job 负责将数据从内存写入持久化存储。

- **`concurrence_limit`**:  
  定义可以同时运行的最大`flush`作业数。限制这一数值可以确保系统不会因多个刷新操作同时进行而过载。  
  - **默认值**：`3`。
  - **示例**：`concurrence_limit = 3`。

- **`queue_limit`**:  
  指定等待执行的最大待处理刷新作业数。这可以防止系统排队过多作业，从而导致性能下降。  
  - **默认值**：`10000`。
  - **示例**：`queue_limit = 10000`。

## 垃圾回收（GC）作业配置

垃圾回收作业用于删除未使用或过时的数据，以确保资源的有效使用。

- **`concurrence_limit`**:  
  定义可以同时运行的垃圾回收作业数。这通常保持较低，以避免在关键操作期间影响系统性能。  
  - **默认值**：`1`。
  - **示例**：`concurrence_limit = 1`。

- **`queue_limit`**:  
  确定在给定时间可以排队的垃圾回收作业数。  
  - **默认值**：`10000`。
  - **示例**：`queue_limit = 10000`。

## 集群Compact非活动作业配置

集群压缩对集群中的数据进行重组和优化。这有助于提高存储和检索的效率。

- **`concurrence_limit`**:  
  指定可以同时运行的最大 `cluster compact inactive` 作业数。压缩是资源密集型操作，因此通常会被少量运行以避免影响性能。  
  - **默认值**：`1`。
  - **示例**：`concurrence_limit = 1`。

这些配置确保了系统作业如刷新、垃圾回收和压缩的良好管理，提供最佳性能，同时防止资源过载。
