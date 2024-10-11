# Small Models, Big Insights: Leveraging Slim Proxy Models to Decide When and What to Retrieve for LLMs

**Authors**: Jiejun Tan, Zhicheng Dou, Yutao Zhu, Peidong Guo, Kun Fang, Ji-Rong Wen  
**Affiliation**: Gaoling School of Artificial Intelligence, Renmin University of China, Baichuan Intelligent Technology

## Research Background

1. **Research Problem**: This paper discusses how to balance the trade-offs between retrieval and answer generation in large language models (LLMs). Current methods often rely on explicit retrieval mechanisms, which can lead to increased computational costs.
   
2. **Research Goal**: The core of this research is how to efficiently determine when retrieval is necessary, while also improving the accuracy and performance of LLMs during the retrieval process without increasing the computational burden.

3. **Related Work**: This problem stems from the area of Retrieval-Augmented Generation (RAG). Existing methods are effective but often lead to higher costs and can suffer from inefficiencies in retrieval decision-making.

## Research Method

This paper proposes a new method called **SlimPLM**, which addresses the issue of determining when and what information should be retrieved in LLMs. Specifically:

1. **Proxy Model to Generate Heuristic Answer**: A lightweight **proxy model** is used to generate an initial **heuristic answer**. This answer serves two purposes:  
   (1) To determine whether retrieval is needed;  
   (2) To provide an answer when retrieval is unnecessary.

   ![image](https://github.com/user-attachments/assets/304edfc3-3402-495d-9617-efedc9f5dc91)


2. **Necessity of Retrieval Judgment**: The heuristic answer is evaluated to judge whether further retrieval is necessary. If the heuristic answer is of high quality, the LLM directly uses it as the final answer; otherwise, retrieval is triggered.

3. **Query and Filtering**: Based on the heuristic answer, the model breaks the question into multiple claims, filtering those that require retrieval through a time-based mechanism.

   The method is defined by the following formula:

   $$
   \hat{a} = PM(x)
   $$

   where \(x\) is the input query, and \(\hat{a}\) is the heuristic answer generated by the proxy model.

   **Heuristic Answer**: `{Heuristic Answer}`  
   **Question**: `{user question}`
![image](https://github.com/user-attachments/assets/675163da-045b-48eb-890f-00de97615c96)

## Experimental Setup

1. **Datasets**: Experiments were conducted on five popular QA datasets: Natural Questions (NQ), TriviaQA, ASQA, MuSiQue, and ELI5.

2. **Evaluation Metrics**:  
   - For long-form answers, the **Rouge Score (ROUGE)** was used to evaluate quality.  
   - For fact-based answers, **Exact Match (EM)** was employed.

3. **Baselines**: Several methods were used for comparison, including different prompting strategies (Vanilla Chat, Chain-of-Thought Prompting) and several retrieval-enhanced methods (Direct RAG, FLARE, Self-Eval, Self-Ask/RSKR-KNN).

4. **Models**: The experiments used LLMs such as **Llama2-70B**, **ChatGPT**, and **PaLM-2**, comparing their performance against SlimPLM.

## Results and Analysis

1. **Overall Results**: SlimPLM showed superior performance in reducing reliance on explicit retrieval, resulting in more efficient answer generation.

2. **Detailed Results**: In multiple datasets, SlimPLM was able to generate high-quality answers without the need for explicit retrieval, demonstrating the model's efficiency.

3. **Computational Costs**: SlimPLM's computation cost was only one-third or one-fourth of the original LLM inference cost, proving its effectiveness.

4. **Ablation Study**: Ablation experiments validated the importance of query necessity, retrieval judgment, and claim-based query filtering mechanisms.

![image](https://github.com/user-attachments/assets/dc17ffb4-0f6e-46f4-a60f-b4155f14085d)


## Conclusion

This paper introduces a new RAG paradigm, leveraging Slim Proxy Models to efficiently decide when retrieval is necessary and generating heuristic answers for LLMs. The results show a significant improvement in both performance and computational efficiency, providing a new direction for knowledge retrieval in LLMs.



