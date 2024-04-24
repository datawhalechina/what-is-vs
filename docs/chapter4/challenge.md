## 4.2 向量数据库面临的挑战



### 动态数据集

Highly concurrent vector search with addition and deletion. Most existing vector search systems build
indices offline and become read-only once deployed. In some applications, data capture may occur more
frequently than query processing, or the application may need to index continuous data streams while serving
query requests. In these cases, the index organization should be optimized for addition and update in addition to
query performance. The complexity arises with concurrent read and update operations (e.g., addition, deletion), as
it is challenging to achieve both correctness and speed simultaneously. Concurrent updates and reads can lead to
data races, making it difficult to ensure correctness on shared-memory architectures. Lock-based synchronization
33can be used to coordinate access to shared-memory data, but while using one lock for the entire index simplifies
reasoning about correctness, it also leads to serialized execution, severely impacting scalability. Another solution
is to use fine-grained locking, where multiple locks are associated with the index. However, fine-grained locking
increases the complexity of operations that access shared data, leading to issues such as deadlock, atomicity
violation, and high locking overhead. The research opportunity here is: Build a highly concurrent vector search
system that supports robust addition and deletion with high search efficiency.

### 索引构建自动化

Automating index construction for vector search. Several advances have been made in support of largescale vector search, introducing novel algorithms and system optimizations [ 15, 51, 55, 66]. However, applying
these methods to large-scale datasets still requires a significant amount of engineering effort specific to the data,
hardware environment, and performance objectives. For instance, deploying a large dataset to a given cloud VM
requires a careful selection of vector search indices, with NVMe/SSD/remote storage, the number of cores to
use, and multiple index-specific parameters. Correctly choosing the algorithm and tuning the parameters can
deliver significant improvements in search performance but also depend on strong system expertise. Therefore,
automating the selection and construction of vector search indices would help alleviate the burden on deployment
engineers, but it also requires navigating a complex space of choices that grows exponentially with different
algorithm choices, each with its own trade-offs, and data sizes and hardware resources. The research opportunity
here is: Build a framework and optimization algorithm that automatically finds the optimal index construction
strategy for a given dataset to deliver fast search speed with low cost.



### 基于硬件的加速

@田冰？  http://sites.computer.org/debull/A23sept/p22.pdf  P12 Research Challenge 1



