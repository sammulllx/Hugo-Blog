---
title: "人工智能"
date: 2024-15-18T00:57:49+08:00
# weight: 1
# aliases: ["/first"]
tags: ["ai"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
# 情感识别

## 问题

本文主要研究产品情感原因分析任务，旨在从产品评论中找到某些情感的本质原因。目前的研究只研究文本中某些spans（张成子空间）的显性原因，但一些关键和有用的原因可能表达得很模糊，它们可能没有提及，但可以从文本语义学中推断出来，它们可以捕捉到深层原因，解释一些未知现象，从而为市场研究和产品优化等应用提供有利支持。 为了解决这个问题，我们在本文中提出了一项新的情感隐含原因发现（EICD）任务。 我们开发了一种新颖的方法，可以根据上下文和常识知识推断出隐含原因。 我们的方法首先从大型语言模型中检索相关知识，构建情感和潜在原因的推理图。 然后，我们对图中的结构知识进行编码，并通过演绎推理推断出隐含原因。 为了评估我们的方法，我们根据亚马逊产品评论构建了一个名为EICDset的大型数据集。 对其进行的实验证明了我们模型的有效性



## 方法

提出了一项新任务--"情绪隐含原因发现（EICD）"。它旨在从评论中找出引发情绪的隐含原因，现有的工作大多集中在显性原因上， 而忽略了隐含在文本语义中的未表达原因的重要性。此外，基于提取的传统方法缺乏灵活性，无法处理非跨度原因识别。为了解决这个问题，我们开发了一种新方法，它可以根据上下文和人类共享知识推导出隐含原因。具体来说，我们从大型语言模型和知识库中检索相关的常识内容，以弥补原因事件和隐含原因之间的知识差距。然后，我们构建了从情绪到潜在隐含原因的推理路径。我们使用图神经网络对分句的结构性内容进行编码。为了评估我们方法的有效性，我们构建了一个基于亚马逊产品评论的大型语料库。我们对其进行了实验，以证明我们模型的有效性。



我们为 EICD 任务提出了一种新颖的情感隐含原因生成模型。含若干条款和与之对应的情感 *e*。我们将发现情绪的隐含原因视为文本生成任务，使用基于常识推理的模型生成触发情绪的隐含原因。

我们模型的整体架构如图所示，它由三个主要部分组成：基于常识的语义图构建模块（CSG）、情感和原因图表示模块（ECG），以及隐因生成模块（ICG）。我们首先将文档 *D* 中的所有分句作为模型的输入。随后，CSG 模块通过分析给定文档中的语义关系和相关常识知识，构建出原因条款和潜在情感条款的语义图。ECG 模块在结合常识知识和上下文语义的同时，对图的结构特征进行表征。ICG 模块首先识别情绪和原因的重要候选组合，然后找出它们之间关联性很强的因果组合，最后对隐含原因进行解码。每个模块的结构如下。

## 改进思路

在未来的工作中，我们将进一步提高模型的性能和可靠性。此外，我们还将扩展其应用场景，以提高其实用性。

### 


