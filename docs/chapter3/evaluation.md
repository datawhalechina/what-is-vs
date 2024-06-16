# 基于Ragas的RAG评价体系

这里将以[《动手学深度学习》](https://zh.d2l.ai/)一书为例，演示如何基于[Ragas](https://docs.ragas.io/en/stable/)的RAG评价体系，框架选择为[`Langchain`](https://www.langchain.com/)。

## 回答生成

以下代码源自`evaluation.py`

### 第三方库导入

```python
import os
import pandas as pd
from langchain_community.document_loaders import DirectoryLoader
from ragas.testset.generator import TestsetGenerator
from ragas.testset.evolutions import simple, reasoning, multi_context
from langchain_openai import ChatOpenAI, OpenAIEmbeddings
from langchain_community.chat_models import ChatOllama
import os
```

### 路径配置

```python
DATA_PATH = "d2l-en-master/chapter_natural-language-processing-applications"
```

### 环境变量

```python
def setup_environment():
    os.environ["OPENAI_API_KEY"] = os.environ.get('OPENAI_API_KEY')
    print("Environment set up with OpenAI API key.")
```

### 读入文件

使用 `DirectoryLoader` 类从指定目录（`DATA_PATH`）加载 Markdown 文件。这些文件包含自然语言处理应用的相关内容，将作为后续生成测试集的基础。加载完成后，函数会打印出加载文档的数量，以便跟踪处理的文档规模。

```python
def load_documents():
    loader = DirectoryLoader(DATA_PATH, glob="**/*.md")
    documents = loader.load()
    print(f"Loaded {len(documents)} documents.")
    return documents
```

###  测试集生成器

初始化一个测试集生成器，它配置了两种不同的语言模型：`ChatOpenAI` （特定配置为 "gpt-3.5-turbo-16k"）用于生成测试内容，而 `ChatOpenAI`（特定配置为 "gpt-4"）用作评价这些内容的模型。同时，使用 `OpenAIEmbeddings` 提供文本嵌入功能，这些嵌入用于在生成测试时提升内容的相关性和准确性。

```python
def create_testset_generator():
    generator_llm = ChatOpenAI(model="gpt-3.5-turbo-16k")
    critic_llm = ChatOpenAI(model="gpt-4")
    embeddings = OpenAIEmbeddings()
    generator = TestsetGenerator.from_langchain(generator_llm, critic_llm, embeddings)
    print("Test set generator created.")
    return generator
```

### 合成测试集

调用前面创建的测试集生成器，根据加载的文档生成一个合成的测试集。可以通过 `distributions` 参数控制不同类型问题（如简单问题、推理问题和多上下文问题）的生成比例。这样不仅丰富了测试集的内容，也使得测试能覆盖更广泛的场景。

```python
def generate_test_set(documents, test_size=10):
    generator = create_testset_generator()
    distributions = {
        simple: 0.5,
        reasoning: 0.25,
        multi_context: 0.25
    }
    testset = generator.generate_with_langchain_docs(documents, test_size, distributions)
    print(f"Generated test set with {test_size} questions.")
    return testset
```

### 格式转换

将测试集转换为 pandas 的 DataFrame 格式。使得生成的数据可以更方便地进行进一步的分析和处理，也方便查看和验证生成内容的结构和质量。

```python
def export_to_dataframe(testset):
    test_df = testset.to_pandas()
    print("Test set exported to DataFrame.")
    return test_df
```

### 文件保存

将 DataFrame 保存为 CSV 文件，这不仅为测试集提供了一种持久的存储格式，也便于分享和在其他应用中使用。

```python
def save_to_csv(test_df, filename):
    test_df.to_csv(filename, index=False)
    print(f"Test set saved to {filename}.")
```

### `main`函数

将上述提到的函数在 `main` 中进行调用

```python
def main():
    setup_environment()
    documents = load_documents()
    testset = generate_test_set(documents)
    test_df = export_to_dataframe(testset)
    save_to_csv(test_df, "test_set.csv")

if __name__ == "__main__":
    main()
```

### 代码执行

在Windows Powershell中执行 `python evaluation.py`，待运行完成即可