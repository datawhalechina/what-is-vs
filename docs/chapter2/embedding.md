# 2.1 向量嵌入
向量嵌入（Embedding）是人工智能领域中一项基础且至关重要的技术。它将复杂的数据（如单词、短语、句子甚至整个文档）映射到高维向量空间中，使得这些数据在向量空间中的相对位置能够反映它们在语义空间中的相似性。在这个过程中，我们将实体转化为了一种可以被计算机理解和处理的形式，即向量。这种转化过程通常涉及到大量的数据和嵌入算法。

# 2.1.1 Embedding的定义
在自然语言处理中，嵌入向量，或称为“Embedding”，是一种将离散型变量转化为连续向量的技术。在这个过程中，每个离散型实体都被分配给一个向量，这个向量就是用于表征这个实体的嵌入向量。这些嵌入向量通常由模型学习得到，而学习的目标是使得语义相近的实体在嵌入空间中有相近的位置。例如，在词嵌入中，意思相近的单词被映射到向量空间中的相近位置。

嵌入向量的维度通常远小于原始实体的数量，比如在处理英文单词时，英文单词的总数量可能有几十万，而嵌入向量的维度通常在几十到几百之间。通过这种方式，嵌入技术实现了对原始实体的压缩表示，大大降低了处理复杂实体的计算复杂性。

# 2.1.2 为什么需要Embedding

在机器学习的众多任务中，我们需要计算机帮我们处理大量的离散数据，如用户特征、商品信息、长文本、表格等。然而，这些离散数据基本无法直接作为计算机的输入，因为这些数据类型是于计算机不可理解的。例如，计算机无法直接理解单词的含义，也无法直接比较两个用户或两个商品的相似性。为了解决这个问题，我们需要将这些离散数据转化为计算机可以理解的形式，即数值型向量，这就是嵌入向量的任务。

通过嵌入向量，我们可以将离散数据的相似性转化为向量的相似性，这样就可以利用向量空间中的各种操作来计算实体的相似性、进行分类、聚类等任务。例如，在推荐系统中，我们可以通过计算用户和商品的嵌入向量的相似性来预测用户对商品的喜好程度；在自然语言处理中，我们可以通过计算单词的嵌入向量的相似性来预测单词的语义相似性。

# 2.1.3 自然语言处理中经典的Embedding算法

# 2.1.3.1 词袋模型
是一种早期的处理文本数据的方法，虽然它的处理方式很简单。但它为后续的嵌入方法铺平了道路。在词袋模型中，每个文档被表示为一个向量，向量的长度等于词汇表的大小，每个元素表示该词在文档中出现的次数。例如，假设我们有一个词汇表：{"我", "爱", "你", "他"}，然后有一个句子"我爱你"，那么这个句子的词袋表示就是[1, 1, 1, 0]。这种方法的主要问题是它忽略了词序，且无法捕获词义。

# 2.1.3.2 Word2Vec
随着学者们对深度学习技术的不断探索，Word2Vec算法在2013年被Google提出。它使用神经网络学习词向量，使得语义上相似的词在向量空间中靠近。Word2Vec有两种主要的训练方法：CBOW（Continuous Bag of Words）和Skip-Gram。CBOW通过上下文预测中心词，而Skip-Gram通过中心词预测上下文。例如，对于句子"我爱你"，如果我们选择"爱"作为中心词，那么CBOW任务就是通过["我",  "你"]来预测"爱"，而Skip-Gram任务就是通过"爱"来预测["我", "你"]。虽然这种方法提出后，被广泛的应用，但由于它只能考虑固定窗口大小的上下文。所以在一些任务中仍然有局限性。

# 2.1.3.3 Bert
Google在2018年提出了BERT。BERT使用了Transformer模型，它可以捕获句子中所有词的上下文信息。为什么我们需要通过完整的上下文信息来生成Embedding向量呢？其实它的工作方式和人类类似，在理解一句话的时候，它不是局限于某个词本身，而是结合上下文的其他词以及这个词在句子中的位置。这样Bert就能够理解这个词在句子中的真正含义了。  
例如，我们来看"苹果"这个词。在"我喜欢吃苹果"这个句子中，"苹果"指的是一种水果。但是在"我在使用苹果电脑"这个句子中，"苹果"指的是一个电子产品品牌。  
如果我们只看"苹果"这个词，我们无法确定它的具体含义。但是，如果我们同时看"苹果"前后的词，我们就可以准确地理解它的含义。这就是Bert的工作方式。当然，这类模型的训练复杂度是更高的，需要大量的训练资源。


# 2.1.4 大模型时代下的Embedding模型
在大模型时代下，需要新的Embedding模型来应对大规模数据处理、多模态任务以及复杂任务的需求。现有的Embedding模型虽然已经非常强大，但在面对更加复杂的场景时，仍然需要进一步的优化和创新。例如，多语言、多模态的却需求。

# 2.1.4.1 多模态Embedding模型
一个典型的多模态Embedding模型的例子是CLIP（Contrastive Language-Image Pretraining）。CLIP由OpenAI在2021年提出，其核心理念是通过图文对比学习预训练，将图像和文本进行关联，从而实现跨模态特征相似度计算、零样本图片分类等任务。CLIP通过对比学习的方法，使得图像中的“小狗”和文本中的“小狗”能够生成相似的Embedding向量，从而实现了模态对齐。
CLIP模型在跨模态特征相似度计算方面的具体实现机制主要通过以下步骤设计：
编码器转换：在训练阶段，CLIP使用大量的文本图像配对数据进行训练。通过编码器将图像和文本转换为特征向量。这些特征向量分别代表了图像和文本的高维表示。

内积计算相似度：CLIP通过计算图像和文本特征向量的内积来衡量它们之间的相似度。这种方法使得模型能够在统一的向量空间中直接进行跨模态的特征相似度计算。

对比学习预训练：CLIP的训练分为三个阶段，其中对比式预训练阶段使用图像-文本对进行对比学习，进一步优化模型的性能。

规范化处理：为了减少偏差，CLIP在实际应用中会对编码后的特征向量进行规范化处理。

```python
import torch
from transformers import CLIPProcessor, CLIPModel
from PIL import Image
import requests

# 加载模型和处理器
model = CLIPModel.from_pretrained("openai/clip-vit-base-patch32")
processor = CLIPProcessor.from_pretrained("openai/clip-vit-base-patch32")

# 准备图像和文本
image_url = "https://example.com/dog.jpg"  
image = Image.open(requests.get(image_url, stream=True).raw)
texts = ["A photo of a dog", "A photo of a cat"]

# 处理图像和文本
inputs = processor(text=texts, images=image, return_tensors="pt", padding=True)

# 获取图像和文本的嵌入向量
outputs = model(**inputs)
image_features = outputs.image_embeds
text_features = outputs.text_embeds

# 计算图像和文本特征向量的相似度
logits_per_image = outputs.logits_per_image # 图像与文本之间的相似度
logits_per_text = outputs.logits_per_text   # 文本与图像之间的相似度

# 输出相似度
print(logits_per_image)
print(logits_per_text)

```

# 2.1.4.2 多语言Embedding模型
多语言表征模型的应用场景比较广泛。Microsoft的E5多语言嵌入模型。该模型在零样本和多语言设置中具有最先进的性能，并且可以在Elasticsearch中使用来进行多语言向量搜索。此外，OpenAI也发布了新一代的多语言嵌入模型embedding v3，这些模型分为较小的text-embeddings-3-small和较大且功能更强大的text-embeddings-3-large，具有更高的多语言性能。这些模型能够处理多种语言的文本，并在实际应用中提供高质量的向量表示。

OpenAI发布的多语言嵌入模型v3与前一版本相比有以下改进：

更高的多语言性能：v3版本的嵌入模型被描述为性能最好的嵌入模型，具有更高的多语言性能。

模型分类：v3版本的嵌入模型分为两类，分别是较小且高效的text-embedding-3-small模型和更大且功能更强大的text-embedding-3-large模型。

使用MRL技术：在v3嵌入API中，默认使用MRL（粗粒度到细粒度的检索）技术用于检索和RAG（检索增强生成），这使得模型在处理复杂任务时更加高效和灵活。

```python
import openai

# 设置API密钥
openai.api_key = "your-api-key"  

# 文本列表（不同语言）
texts = [
    "This is an English sentence.",
    "这是一个中文句子。",
    "C'est une phrase en français."
]

# 获取嵌入向量
response = openai.Embedding.create(
  model="text-embedding-3-large",
  input=texts
)

# 输出嵌入向量
for i, embedding in enumerate(response['data']):
    print(f"Text: {texts[i]}")
    print(f"Embedding: {embedding['embedding']}\n")
```

# 2.1.5 总结
总的来说，Embedding技术是AI的基石技术，甚至可以说Embedding技术的发展对AI的能力表现起到决定作用。在本章中，我们按照时间顺序介绍了几种经典的算法。这些算法虽然表征的方法不同，但它们的基础是概率和统计学，都试图从大量的文本数据中学习词的语义。这些方法为我们提供了处理和理解自然语言的强大工具，它们在许多NLP任务中，如文本分类、情感分析、命名实体识别等，都发挥了关键作用。

