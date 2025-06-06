---
{"dg-publish":true,"permalink":"/contriever-ir-course-assignment/"}
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
***
##### 2. 评价指标

**信息检索**的评价指标，包括Recall、Accuracy、Precision、MAP、MRR、NDCG等，在contriever中主要关注 Recall 和 NDCG，并针对 Top-k 个结果进行计算，即以 Recall@k 和 NDCG@k 作为评价指标。

给定一组查询 $\mathcal{Q}=\{q_1, q_2, \ldots, q_n\}$，和一组文档 $\mathcal{D}=\{d_1, d_2, \ldots, d_m\}$。对于每个查询 $q$，检索模型会计算 $q$ 和 $\mathcal{D}$ 中每个文档的相关度值，即 $s(q,\mathcal{D})=\{ s(q, d_1), s(q, d_2), \ldots, s(q, d_m) \}$

**Recall@k**：
- 定义：对于给定的查询 $q$，我们以 $s(q,\mathcal{D})$ 中得分最高的前 $k$ 个文档作为检索结果，$\text{Recall@}k$ 旨在计算 检索结果中和查询 $q$相关的文档数，占 文档集 $\mathcal{D}$ 中和查询 $q$相关的文档数 的比值。
- 若以$\# \text{ rel}_{q}$ 作为 $\mathcal{D}$ 中所有和查询 $q$ 相关的文档；以 $\# \text{ retr}_{q,k}$ 作为检索结果中，真正和查询 $q$ 相关的文档，则可得如下公式：
$$\text{Recall@}k=\frac{\# \text{ retr}_{q,k}}{\# \text{ rel}_{q}}$$
- 由于我们需要评估一组查询 $\mathcal{Q}$，故对 单个查询 $q$ 的 $\text{Recall@}k$ 值进行求和取平均，得到最终公式如下所示：
$$\text{Recall@}k=\frac{1}{|\mathcal{Q}|}\sum_{q=1}^{|\mathcal{Q}|}\frac{\# \text{ retr}_{q,k}}{\# \text{ rel}_{q}}$$

**NDCG@k**：全称为 Normalize Discounted Cumulative Gain，其公式如下：
$$\text{NDCG@}k=\frac{1}{|\mathcal{Q}|}\sum_{q=i}^{|\mathcal{Q}|}\frac{\text{DCG}_q\text{@}k}{\text{IDCG}_q\text{@}k}$$
- Gain：给定查询 $q$ 和 文档集 $\mathcal{D}$， $q$ 和 $\mathcal{D}$ 中的每个文档 $d_i$ 可评测出一个**真实的相关性得分**，即为Gain，这一组相关性得分通常用 $rel=[gain_1, gain_2, \ldots, gain_m]$ 进行表示。

- CG(Cumulative Gain)：将检索结果的相关性评分累加起来，不考虑检索结果的排序。如果指定 $k$，则以 $s(q,\mathcal{D})$ 中得分最高的前 $k$ 个文档作为检索结果，并只累计它们的相关性评分。这里以 $rel_i$ 作为 查询 $q$  和 检索结果中第 $i$ 个文档 的 相关性分数
$$\text{CG@}k=\sum_i^k{rel_{i}}$$
- DCG(Discounted Cumulative Gain)：对CG的一种改进，通过引入位置折扣因子$\frac{1}{log_2(i+1)}$来考虑检索结果的排序，给定 $k$ 时，则有下式：
$$\text{DCG@} k = \sum_{i=1}^{k} \frac{\text{rel}_i}{\log_2(i+1)}$$
- IDCG(Ideal Discounted Cumulative Gain):：最理想的检索结果，即检索结果为 $rel$ 降序排列后的顺序，给定 $k$ 时，则取降序排列后的 $rel$ 的前 $k$ 个 gain 进行计算，计算公式同 DCG。

注：由于 $s(q,\mathcal{D})$ 中可能存在并列分数，但它们对应的相关性得分不一定相同，因此检索结果可能存在不同排序，这时 DCG 的计算结果也将不一致。故在 NDCG@k 实现过程中一个小 trick，即先对 doc_id 进行降序排列，确保 doc_id 顺序的一致性，这样实现的结果才会和 官方结果 一致

参考：
- \[1\] [信息检索中的评价指标](https://zhuanlan.zhihu.com/p/588901292#:~:text=%E4%BB%8B%E7%BB%8D%E5%9C%A8retrieval-ranking%E4%B8%AD%E8%A1%A1%E9%87%8F%20%E6%A8%A1%E5%9E%8B%E6%95%88%E6%9E%9C%20%E7%9A%84%E6%8C%87%E6%A0%87%EF%BC%8C%E5%8C%85%E6%8B%AC%20Recall%2C,Accuracy%2C%20Precision%2C%20MAP%2C%20MRR%E5%92%8CNDCG%E3%80%82%20%E6%B3%A8%EF%BC%9A%E5%AF%B9%E4%BA%8E%E6%A3%80%E7%B4%A2%E7%BB%93%E6%9E%9C%EF%BC%8C%E9%80%9A%E5%B8%B8%E6%8E%92%E5%BA%8F%E9%9D%A0%E5%89%8D%E7%9A%84%E7%BB%93%E6%9E%9C%E5%BE%80%E5%BE%80%E6%9B%B4%E5%8A%A0%E9%87%8D%E8%A6%81%EF%BC%8C%E5%9B%A0%E6%AD%A4%E8%BF%99%E4%BA%9B%E8%AF%84%E4%BB%B7%E6%8C%87%E6%A0%87%E9%83%BD%E4%BC%9A%E9%92%88%E5%AF%B9top-k%E7%BB%93%E6%9E%9C%E8%BF%9B%E8%A1%8C%E8%AE%A1%E7%AE%97%EF%BC%88%E8%AE%B0%E4%BD%9C%40k%EF%BC%89%E3%80%82)
- \[2\] [谈谈NDCG的计算](https://zhuanlan.zhihu.com/p/674064579)
***
##### 3. 实验结果

[contriever](https://github.com/facebookresearch/contriever)提供了多个预训练模型，但我们只要使用在 CCnet 和 English Wikipedia 上无监督预训练得到的权重 ```facebook/contriever```，完成下面这些 Dataset 上的实验即可。

<div style="text-align:center"> <strong>表2：</strong> 实验结果</div>
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
		<td align="center">  </td>
		<td align="center"> </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center"> Bio-Medical</td>
		<td align="center"> NFCorpus</td>
		<td align="center">323 </td>
		<td align="center"> 3.6K</td>
		<td align="center">  </td>
		<td align="center"> </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center" rowspan="1">Question Answering (QA)</td>
		<td align="center">Finance</td>
		<td align="center"> FiQA-2018</td>
		<td align="center">648 </td>
		<td align="center">57K</td>
		<td align="center">  </td>
		<td align="center">  </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center" rowspan="1">Argument Retrieval</td>
		<td align="center">Misc.</td>
		<td align="center"> ArguAna</td>
		<td align="center">1,406 </td>
		<td align="center"> 8.67K</td>
		<td align="center"> </td>
		<td align="center"> </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center">Duplicate-Question Retrieval</td>
		<td align="center">Quora</td>
		<td align="center"> Quora</td>
		<td align="center">10,000 </td>
		<td align="center"> 523K</td>
		<td align="center">  </td>
		<td align="center">  </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center">Citation-Prediction</td>
		<td align="center">Scientific</td>
		<td align="center"> SCIDOCS</td>
		<td align="center">1,000 </td>
		<td align="center"> 25K</td>
		<td align="center">  </td>
		<td align="center">  </td>
		<td align="center"> </td>
	</tr>
	
	<tr>
		<td align="center">Fact Checking</td>
		<td align="center">Scientific</td>
		<td align="center"> SciFact</td>
		<td align="center">300 </td>
		<td align="center"> 5K</td>
		<td align="center">  </td>
		<td align="center">  </td>
		<td align="center"> </td>
	</tr>
</table>

***
