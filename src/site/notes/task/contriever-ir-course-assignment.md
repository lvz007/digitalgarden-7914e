---
{"dg-publish":true,"permalink":"/task/contriever-ir-course-assignment/"}
---

##### 1. 数据集介绍

<div style="text-align:center"> <strong>表1：</strong> <a href="https://github.com/beir-cellar/beir/tree/main">BEIR</a> 数据集介绍</div>

| Dataset       | Website                                                                                  | BEIR-Name          | Queries | Corpus | Rel D/Q |                                            Download                                             |
| ------------- | ---------------------------------------------------------------------------------------- | ------------------ | ------- | ------ | ------- | :---------------------------------------------------------------------------------------------: |
| MSMARCO       | [Homepage](https://microsoft.github.io/msmarco/)                                         | `msmarco`          | 6,980   | 8.84M  | 1.1     |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/msmarco.zip)      |
| TREC-COVID    | [Homepage](https://ir.nist.gov/covidSubmit/index.html)                                   | `trec-covid`       | 50      | 171K   | 493.5   |    [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/trec-covid.zip)    |
| NFCorpus      | [Homepage](https://www.cl.uni-heidelberg.de/statnlpgroup/nfcorpus/)                      | `nfcorpus`         | 323     | 3.6K   | 38.2    |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/nfcorpus.zip)     |
| NQ            | [Homepage](https://ai.google.com/research/NaturalQuestions)                              | `nq`               | 3,452   | 2.68M  | 1.2     |        [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/nq.zip)        |
| HotpotQA      | [Homepage](https://hotpotqa.github.io/)                                                  | `hotpotqa`         | 7,405   | 5.23M  | 2.0     |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/hotpotqa.zip)     |
| FiQA-2018     | [Homepage](https://sites.google.com/view/fiqa/)                                          | `fiqa`             | 648     | 57K    | 2.6     |       [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/fiqa.zip)       |
| ArguAna       | [Homepage](http://argumentation.bplaced.net/arguana/data)                                | `arguana`          | 1,406   | 8.67K  | 1.0     |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/arguana.zip)      |
| Touche-2020   | [Homepage](https://webis.de/events/touche-20/shared-task-1.html)                         | `webis-touche2020` | 49      | 382K   | 19.0    | [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/webis-touche2020.zip) |
| CQADupstack   | [Homepage](http://nlp.cis.unimelb.edu.au/resources/cqadupstack/)                         | `cqadupstack`      | 13,145  | 457K   | 1.4     |   [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/cqadupstack.zip)    |
| Quora         | [Homepage](https://www.quora.com/q/quoradata/First-Quora-Dataset-Release-Question-Pairs) | `quora`            | 10,000  | 523K   | 1.6     |      [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/quora.zip)       |
| DBPedia       | [Homepage](https://github.com/iai-group/DBpedia-Entity/)                                 | `dbpedia-entity`   | 400     | 4.63M  | 38.2    |  [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/dbpedia-entity.zip)  |
| SCIDOCS       | [Homepage](https://allenai.org/data/scidocs)                                             | `scidocs`          | 1,000   | 25K    | 4.9     |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/scidocs.zip)      |
| FEVER         | [Homepage](http://fever.ai/)                                                             | `fever`            | 6,666   | 5.42M  | 1.2     |      [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/fever.zip)       |
| Climate-FEVER | [Homepage](http://climatefever.ai/)                                                      | `climate-fever`    | 1,535   | 5.42M  | 3.0     |  [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/climate-fever.zip)   |
| SciFact       | [Homepage](https://github.com/allenai/scifact)                                           | `scifact`          | 300     | 5K     | 1.1     |     [Link](https://public.ukp.informatik.tu-darmstadt.de/thakur/BEIR/datasets/scifact.zip)      |

数据集目录结构:
```
BEIR-Name/ 
├── qrels/ 
│ └── test.tsv  #  query-id    corpus-id   score
├── corpus.jsonl  # {"_id": , "title": ,"text": , "metadata": } 
└── queries.jsonl  # {"_id": , "text": , "metadata": } 
```


数据集可根据给出的链接进行下载；如果数据没下载，在执行下面命令时，会自动下载数据集并解压，但这时`--dataset` 后面得直接跟具体的BEIR-Name，不能 data/BEIR-Name，否则会报错 。
```shell
python eval_beir.py \
    --model_name_or_path facebook/contriever \
    --dataset BEIR-Name  \
    --per_gpu_batch_size 768 
```
[contriever](https://github.com/facebookresearch/contriever)提供了多个预训练模型，但我们只要 fackbook/contriever 的推理结果即可。
***
##### 2. 评价指标

**信息检索**的评价指标，包括Recall、Accuracy、Precision、MAP、MRR、NDCG等，在contriever中主要关注 Recall 和 NDCG，并针对 Top-k 个结果进行计算，即以 Recall@k 和 NDCG@k 作为评价指标。

给定一组查询 $\mathcal{Q}=\{q_1, q_2, \ldots, q_n\}$，和一组文档 $\mathcal{D}=\{d_1, d_2, \ldots, d_m\}$。对于每个查询 $q$，模型会计算其和 $\mathcal{D}$ 中每个文档的相关度值，即 $s(q,\mathcal{D})=\{ s(q, d_1), s(q, d_2), \ldots, s(q, d_m) \}$

**Recall@k**：
- 定义：对于给定的查询 $q$，我们以 $s(q,\mathcal{D})$ 中得分最高的前 $k$ 个文档作为检索结果，$\text{Recall@}k$ 旨在计算 检索结果中和查询 $q$ 相关的文档数，和 文档集 $\mathcal{D}$ 中和查询 $q$ 相关的文档数 的比值。
- 若以$\# \text{ rel}_{q}$ 作为 $\mathcal{D}$ 中所有和查询 $q$ 相关的文档；以 $\# \text{ retr}_{q,k}$ 作为检索结果中，真正和查询 $q$ 相关的文档，则可得如下公式：
$$\text{Recall@}k=\frac{\# \text{ retr}_{q,k}}{\# \text{ rel}_{q}}$$
- 由于我们需要评估一组查询 $\mathcal{Q}$，故对 单个查询 $q$ 的 $\text{Recall@}k$ 值进行求和取平均，得到最终公式如下所示：
$$\text{Recall@}k=\frac{1}{|\mathcal{Q}|}\sum_{q=1}^{|\mathcal{Q}|}\frac{\# \text{ retr}_{q,k}}{\# \text{ rel}_{q}}$$

代码示例:
```python
def recall_k(qrels, results, k=100):
    """计算 Recall@k 指标，即在前 k 个检索结果中找到的相关文档占所有相关文档的比例

    Args:
        qrels (dict): 查询-文档相关性标签字典。
                      格式：{query_id: {corpus_id: score}, ...}
                      在 contriever 中由 GenericDataLoader 读取 qrels\test.tsv 得来

        results (dict): 查询-检索结果字典 
                        格式：{qid: {corpus_id: score}, ...}
                        在 contriever 中由 beir.retrieval.evaluation.EvaluateRetrieval.retrieve(corpus, queries) 得来

        k (int, optional): 考虑的前 k 个检索结果数量。 Defaults to 100.

    Returns:
        float: 所有查询的平均 Recall@k 值。
    """
    total_recall, num_queries = 0.0, 0

    for qid, rels in qrels.items():
        if qid not in results:
            continue

        true_relevant_docs = set(
            docid for docid, score in rels.items() if score > 0
        )
        if not true_relevant_docs:
            continue

        pred_docs_at_k = sorted(
            results[qid].items(), 
            key=lambda item: item[1],  # 根据 q 和 corpus 的 score 降序排列
            reverse=True
        )[:k]
        pred_docs_set = set(docid for docid, _ in pred_docs_at_k)

        hit = pred_docs_set.intersection(true_relevant_docs)
        recall = len(hit) / len(true_relevant_docs)

        total_recall += recall
        num_queries += 1

    return round(total_recall / num_queries, 5) if num_queries > 0 else 0.0
```


**NDCG@k**：全称为 Normalize Discounted Cumulative Gain，其公式如下：
$$\text{NDCG@}k=\frac{1}{|\mathcal{Q}|}\sum_{q=i}^{|\mathcal{Q}|}\frac{\text{DCG}_q\text{@}k}{\text{IDCG}_q\text{@}k}$$
- Gain：给定查询 $q$ 和 文档集 $\mathcal{D}$， $q$ 和 $\mathcal{D}$ 中的每个文档 $d_i$ 可评测出一个**真实的相关性得分**，即为Gain，这一组相关性得分通常用 $rel=[gain_1, gain_2, \ldots, gain_m]$ 进行表示。

- CG(Cumulative Gain)：将检索结果的相关性评分累加起来，不考虑检索结果的排序。如果指定 $k$，则以 $s(q,\mathcal{D})$ 中得分最高的前 $k$ 个文档作为检索结果，并只累计它们的相关性评分。这里以 $rel_i$ 作为 查询 $q$  和 检索结果中第 $i$ 个文档 的 相关性分数
$$\text{CG@}k=\sum_i^k{rel_{i}}$$
- DCG(Discounted Cumulative Gain)：对CG的一种改进，通过引入位置折扣因子$\frac{1}{log_2(i+1)}$来考虑检索结果的排序，给定 $k$ 时，则有下式：
$$\text{DCG@} k = \sum_{i=1}^{k} \frac{\text{rel}_i}{\log_2(i+1)}$$
- IDCG(Ideal Discounted Cumulative Gain):：最理想的检索结果，即检索结果为 $rel$ 降序排列后的顺序，给定 $k$ 时，则取降序排列后的 $rel$ 的前 $k$ 个 gain 进行计算，计算公式同 DCG。

代码示例:
```python
def dcg_at_k(scores):
    return sum(sc / math.log2(i + 1) for i, sc in enumerate(scores, start=1))

def ndcg_k(qrels, results, k=10):
    total_ndcg, num_queries = 0.0, 0

    for qid, rels in qrels.items():
        if qid not in results:
            continue

        pred_docs_at_k = sorted(
            results[qid].items(),
            key=lambda x: (x[1], x[0]),  # 关键:对x[0](即doc_id)的排序,不然结果不一致
            reverse=True
        )[:k]
        pred_scores = [rels.get(docid, 0) for docid, _ in pred_docs_at_k]

        ideal_scores = sorted(rels.values(), reverse=True)[:k]
        
        dcg = dcg_at_k(pred_scores)
        idcg = dcg_at_k(ideal_scores)

        ndcg = dcg / idcg if idcg > 0 else 0
        total_ndcg += ndcg
        num_queries += 1

    return round(total_ndcg / num_queries, 5) if num_queries > 0 else 0.0
```

注：由于 $s(q,\mathcal{D})$ 中可能存在并列分数，但它们对应的相关性得分不一定相同，因此检索结果可能存在不同排序，这时 DCG 的计算结果也将不一致。故在 NDCG@k 实现过程中一个小 trick，即先对 doc_id 进行降序排列，确保 doc_id 顺序的一致性，这样实现的结果才会和 官方结果 一致

参考：
- \[1\] [信息检索中的评价指标](https://zhuanlan.zhihu.com/p/588901292#:~:text=%E4%BB%8B%E7%BB%8D%E5%9C%A8retrieval-ranking%E4%B8%AD%E8%A1%A1%E9%87%8F%20%E6%A8%A1%E5%9E%8B%E6%95%88%E6%9E%9C%20%E7%9A%84%E6%8C%87%E6%A0%87%EF%BC%8C%E5%8C%85%E6%8B%AC%20Recall%2C,Accuracy%2C%20Precision%2C%20MAP%2C%20MRR%E5%92%8CNDCG%E3%80%82%20%E6%B3%A8%EF%BC%9A%E5%AF%B9%E4%BA%8E%E6%A3%80%E7%B4%A2%E7%BB%93%E6%9E%9C%EF%BC%8C%E9%80%9A%E5%B8%B8%E6%8E%92%E5%BA%8F%E9%9D%A0%E5%89%8D%E7%9A%84%E7%BB%93%E6%9E%9C%E5%BE%80%E5%BE%80%E6%9B%B4%E5%8A%A0%E9%87%8D%E8%A6%81%EF%BC%8C%E5%9B%A0%E6%AD%A4%E8%BF%99%E4%BA%9B%E8%AF%84%E4%BB%B7%E6%8C%87%E6%A0%87%E9%83%BD%E4%BC%9A%E9%92%88%E5%AF%B9top-k%E7%BB%93%E6%9E%9C%E8%BF%9B%E8%A1%8C%E8%AE%A1%E7%AE%97%EF%BC%88%E8%AE%B0%E4%BD%9C%40k%EF%BC%89%E3%80%82)
- \[2\] [谈谈NDCG的计算](https://zhuanlan.zhihu.com/p/674064579)
***
##### 3. 实验结果

[contriever](https://github.com/facebookresearch/contriever)提供了多个预训练模型，这里使用的是在 CCnet 和 English Wikipedia 上无监督预训练得到的权重 ```facebook/contriever```。

<div style="text-align:center"> <strong>表2：</strong> 实验结果(RTX3090 24G, batch_size=768)</div>

<table style="display: flex; justify-content: center;">
	<tr>
		<th colspan="5" align="center">数据集信息</th>
		<th colspan="3" align="center">实验结果</th>
	</tr>
	
	<tr>
		<td align="center"> Task </td>
		<td align="center"> Domain </td>
		<td align="center"> Dataset </td>
		<td align="center"> Queries </td>
		<td align="center"> Corpus </td>
		<td align="center"> nDCG @10 </td>
		<td align="center"> Recall @100 </td>
		<td align="center"> 时耗 </td>
	</tr>
	
	<tr>
		<td align="center" rowspan="2">Bio-Medical Information Retrieval (IR)</td>
		<td align="center"> Bio-Medical</td>
		<td align="center"> Trec-COVID</td>
		<td align="center"> 50 </td>
		<td align="center"> 171K</td>
		<td align="center"> 27.4</td>
		<td align="center">3.7</td>
		<td align="center">~12m47s</td>
	</tr>
	
	<tr>
		<td align="center"> Bio-Medical</td>
		<td align="center"> NFCorpus</td>
		<td align="center">323 </td>
		<td align="center"> 3.6K</td>
		<td align="center"> 31.73</td>
		<td align="center">29.41</td>
		<td align="center">~23s</td>
	</tr>
	
	<tr>
		<td align="center" rowspan="2">Question Answering (QA)</td>
		<td align="center">Wikipedia</td>
		<td align="center"> NQ</td>
		<td align="center">3,452 </td>
		<td align="center"> 2.68M</td>
		<td align="center"> 25.4</td>
		<td align="center">77.1</td>
		<td align="center">~1h46m</td>
	</tr>
	
	<tr>
		<td align="center">Finance</td>
		<td align="center"> FiQA-2018</td>
		<td align="center">648 </td>
		<td align="center">57K</td>
		<td align="center"> 24.50</td>
		<td align="center"> 56.19</td>
		<td align="center">~3m54s</td>
	</tr>
	
	<tr>
		<td align="center" rowspan="1">Argument Retrieval</td>
		<td align="center">Misc.</td>
		<td align="center"> ArguAna</td>
		<td align="center">1,406 </td>
		<td align="center"> 8.67K</td>
		<td align="center"> 37.90</td>
		<td align="center"> 90.11</td>
		<td align="center">~40s</td>
	</tr>
	
	<tr>
		<td align="center">Duplicate-Question Retrieval</td>
		<td align="center">Quora</td>
		<td align="center"> Quora</td>
		<td align="center">10,000 </td>
		<td align="center"> 523K</td>
		<td align="center"> 83.49</td>
		<td align="center"> 98.71</td>
		<td align="center">~6m6s</td>
	</tr>
	
	<tr>
		<td align="center">Citation-Prediction</td>
		<td align="center">Scientific</td>
		<td align="center"> SCIDOCS</td>
		<td align="center">1,000 </td>
		<td align="center"> 25K</td>
		<td align="center"> 14.91</td>
		<td align="center"> 35.99</td>
		<td align="center">~2m25s</td>
	</tr>
	
	<tr>
		<td align="center">Fact Checking</td>
		<td align="center">Scientific</td>
		<td align="center"> SciFact</td>
		<td align="center">300 </td>
		<td align="center"> 5K</td>
		<td align="center"> 64.92</td>
		<td align="center"> 92.60</td>
		<td align="center">~30s</td>
	</tr>
</table>

