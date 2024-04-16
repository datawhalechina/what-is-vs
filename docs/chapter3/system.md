# 向量数据库系统概述

## 向量数据库的基本构成与工作原理

## 市面主流向量数据库具体比较

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

