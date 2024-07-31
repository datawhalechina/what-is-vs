# 向量数据库系统概述

前文提到了大量向量检索的概念，当然作为向量检索领域的经典工作就是 Meta（前Facebook）开源的 Faiss，其作为向量检索库被广泛应用到了大量的应用中。而且后续发展的向量数据库的初始版本大部分也是基于该库进行构建。

那我们之前提到向量检索已经解决了很多问题，为什么还需要一个向量数据库呢，这个也是因为业务需求导致：

- 假设 100 亿的向量数据，一台机器放不下这么多的数据，需要多台机器此时数据应该如何划分，如何分别计算再返回最终结果
- 假设 100 亿的向量数据，检索性能如何保证，数据更新后如何保证及时的检索
- 向量检索系统如何保证高可用性，服务不能中断，数据不能丢失
- 等等

这些需求单纯靠向量检索库不能够完全解决问题，如果要基于此完全满足需求的话需要大量的开发工作，所以向量数据库出现就不奇怪了。

## 市面主流向量数据库具体比较

目前市面上的向量数据库或者支持向量检索的系统分为这么几类

- **基于原有数据库拓展**：这种一般是原有 TP、AP、HTAP 的拓展，有的选择增加插件的方式，有的是增加数据类型等等，比较有代表性的例如：Oracle、PGvector、Oceanbase、TiDB、MySCALE 等
- **基于原有数据系统拓展**：这种一般是数据仓库，数据湖，或者 NoSQL 的拓展，比较有代表性的例如：Spark、ElasticSearch、MongoDB 等
- **独立的向量数据库**：这种一版选择将向量数据作为系统的核心，在向量检索的基础上拓展其他能力，比较有代表性的例如：Pinecone、Chroma、Milvus、Weaviate、Qdrant 等

大部分支持向量检索的系统都是自大模型出现之后而增加的能力，但是未来向量检索的发展趋势，究竟是原有系统的拓展，还是独立的向量数据库，目前还没有定论，还需要多年的时间来慢慢验证。

### 基础功能

| 名称 (版本年份)                | 向量维度 | 种类        | 过滤 | Multi-Vec. | Graph | IVF  |
| ------------------------------ | -------- | ----------- | ---- | ---------- | ----- | ---- |
| ChromaDB (2022)                | 1536     | Vec.        | ✓    |            | ✓     |      |
| Manu (2022)                    | 32768    | Vec.+ Ftx.  | ✓    | ✓          | ✓     | ✓    |
| Milvus (2021)                  | 32768    | Vec.+ Ftx.  | ✓    | ✓          | ✓     | ✓    |
| Pinecone (2019)                | 20000    | Vec.        | ✓    | ✓          | ✓     | ✓    |
| Weaviate (2019)                | 65535    | Vec.+ Ftx.  | ✓    | ✓          | ✓     |      |
| Qdrant (2021)                  | 4096     | Vec.+ Ftx.  | ✓    | ✓          | ✓     |      |
| Amazon OpenSearch (v2.9, 2023) | 16000    | Ftx.        | ✓    | ✓          | ✓     | ✓    |
| Elastic Search (v8.0, 2022)    | 4096     | Ftx.        | ✓    | ✓          | ✓     | ✓    |
| AnalyticDB-V (2020)            | ≥512     | Rel.+Ftx.   | ✓    |            | ✓     | ✓    |
| PostgreSQL-pgvector (2021)     | 2000     | Rel.+ Ftx.  | ✓    | ✓          | ✓     | ✓    |
| MongoDB Atlas (v6.0, 2023)     | 2048     | NoSQL+ Ftx. | ✓    |            | ✓     |      |
| MyScale (2023)                 | 1536     | Rel.        | ✓    |            | ✓     |      |

## 参考文献

1. Pan J J, Wang J, Li G. Survey of vector database management systems[J]. arXiv preprint arXiv:2310.14021, 2023.
2. Han Y, Liu C, Wang P. A comprehensive survey on vector database: Storage and retrieval technique, challenge[J]. arXiv preprint arXiv:2310.11703, 2023.
3. Jing Z, Su Y, Han Y, et al. When Large Language Models Meet Vector Databases: A Survey[J]. arXiv preprint arXiv:2402.01763, 2024.

