# Machamp

Machamp is a Benchmarking for the task of Generalized Entity Matching (GEM), which aims at performing entity matching between entries in structured, semi-structured, and unstructured format. 

## Task Description

* Rel-HETER: This task is for matching between structured tables with heterogeneous schema. The source is the Fodors-Zagats task from the [Deep Matcher](https://github.com/anhaidgroup/deepmatcher/blob/master/Datasets.md) datasets.

* Semi-HOMO: This task is for matching between semi-structured tables with homogeneous schema. The source is the DBLP-Scholar task from the [Deep Matcher](https://github.com/anhaidgroup/deepmatcher/blob/master/Datasets.md) datasets.

* Semi-HETER: This task is for matching between semi-structured tables with heterogeneous schema. The source is the set of 5 Book tasks from the [Magellan](https://sites.google.com/site/anhaidgroup/useful-stuff/data#TOC-The-784-Data-Sets-for-EM) project.

* Semi-Rel: This task is for matching between semi-structued and structured tables. The source is the set of 5 Movie tasks from the [Magellan](https://sites.google.com/site/anhaidgroup/useful-stuff/data#TOC-The-784-Data-Sets-for-EM) project.

* Semi-Text: This task is for matching between semi-structued and unstructured tables. The source is from the Watch (-w) and Computer (-c) tasks from the [WDC Product Data](http://webdatacommons.org/largescaleproductcorpus/v2/index.html).

* Rel-Text: This task is for matching between structued and unstructured tables. The source is from the DBLP-ACM task from the [Deep Matcher](https://github.com/anhaidgroup/deepmatcher/blob/master/Datasets.md) datasets. The table ACM is replaced with the abstract of the publication.

For more details about the pre- and post-processing of the datasets, please refer to Section 3 and Appendix of [our technique report](https://arxiv.org/abs/2106.08455).

## Data Format
There are 7 benchmarking tasks in total. The name of the folder is corresponding to the task described in the paper. There are 5 files in each dataset folder:
- left: The left table of entities.
- right: The right table of entities.
- train.csv: The training set of pairs
- valid.csv: The validation set of pairs
- test.csv: The test set of pairs

Each table contains an array of records. Based on the format of entities in the left/right tables, the suffix of them can be `.csv` (structured), `.json` (semi-structured) or `.txt` (unstructured).

The instances in train/valid/test files are triplets separated by `\t`: The first item is the id of an entity in the left table, where id means the subscription in the array of records; The second item is the id of an entity in the right table; The third item is the ground truth label (0/1).

## Statistics of Tasks

| Name | Left #Row | Left #Attr | Right #Row | Right #Attr | Train | Valid | Test | % Positive |
|------|-----------|------------|------------|-------------|-------|------|-------|--------------|
| Rel-HETER | 534 | 6.00 | 332 | 7.00 | 567 | 190 | 189 | 11.63 |
| Semi-HOMO | 2616 | 8.65 | 64263 | 7.34 | 17223 | 5742 | 5742 | 18.63 |
| Semi-HETER | 22133 | 12.28 | 23264 | 12.03 | 1240 | 414 | 414 | 38.2 |
| Semi-Rel | 29180 | 8.00 | 32823 | 13.81 | 1309 | 437 | 437 | 41.64 |
| Semi-Text-c | 9234 | 10.00 | 9234 | 1.00 | 5540 | 1846 | 1846 | 11.8 |
| Semi-Text-w | 20897 | 10.00 | 20897 | 1.00 | 12538 | 4180 | 4179 | 14.07 |
| Rel-Text | 2616 | 1.00 | 2295 | 6.00 | 7417 | 2473 | 2473 | 17.96 |

Left/Right #Row denotes the number of rows in the left/right table. Left/Right #Attr means the average number of attributes in the left/right table. Note that the number of attributes in an unstructured table is 1; the number of attributes for different records in a semi-structured table might be different from each other.
## Benchmarking Results

We evaluated 2 traditional machine learning based approaches: SVM and Random Forest; and 5 deep learning approaches: [DeepER](http://www.vldb.org/pvldb/vol11/p1454-ebraheem.pdf), [DeepMatcher](https://dl.acm.org/doi/10.1145/3183713.3196926), [Transformer](https://openproceedings.org/2020/conf/edbt/paper_205.pdf), [SentenceBert](https://aclanthology.org/D19-1410.pdf) and [Ditto](http://www.vldb.org/pvldb/vol14/p50-li.pdf) on the proposed tasks. The results of F1 score are as following.

| | SVM | Random Forest | DeepER | DeepMatcher | Transformer | SentenceBert | Ditto |
|-|-----|---------------|--------|-------------|-------------|--------------|-------|
| Rel-HETER | 0.821 | 0.706 | 0.872 | 0.936 | 0.955 | 0.696 | 1.00 | 
| Semi-HOMO | 0.53 | 0.747 | 0.875 | 0.861 | 0.938 | 0.874 | 0.931 | 
| Semi-HETER | 0.274 | 0.262 | 0.282 | 0.291 | 0.46 | 0.697 | 0.616 | 
| Semi-Rel | 0.709 | 0.733 | 0.436 | 0.567 | 0.905 | 0.59 | 0.911 | 
| Semi-Text-c | 0.557 | 0.65 | 0.418 | 0.442 | 0.886 | 0.798 | 0.818 | 
| Semi-Text-w | 0.556 | 0.505 | 0.388 | 0.427 | 0.665 | 0.502 | 0.649 | 
| Rel-Text | 0.436 | 0.363 | 0.529 | 0.534 | 0.631 | 0.329 | 0.627 | 


## Citation
If you are using the dataset, please cite the following in your work:
```
@inproceedings{cikm21machamp,
  author    = {Jin Wang and
               Yuliang Li and
               Wataru Hirota},
  title     = {Machamp: {A} Generalized Entity Matching Benchmark},
  booktitle = {CIKM},
  year      = {2021}
}
```

## Disclosure

> Jin: Here I just list the source of all the datasets. We might need to ask Eser how to write this part later.
>

* [Deep Martcher](https://github.com/anhaidgroup/deepmatcher/blob/master/Datasets.md): Fodor's and Zagat's restaurant, source is [here](https://www.cs.utexas.edu/users/ml/riddle/data/restaurant.tar.gz)
* [Deep Martcher](https://github.com/anhaidgroup/deepmatcher/blob/master/Datasets.md): citation from Google Scholar, ACM and DBLP, source is [here](https://dbs.uni-leipzig.de/en/research/projects/object_matching/fever/benchmark_datasets_for_entity_resolution)
* [Magellan](https://sites.google.com/site/anhaidgroup/useful-stuff/data#TOC-The-784-Data-Sets-for-EM): The Book datasets are from Amazon, Barnes & Noble, Goodreads and Half. Source is collected by the creater of Magellan project.
* [Magellan](https://sites.google.com/site/anhaidgroup/useful-stuff/data#TOC-The-784-Data-Sets-for-EM): The Movie datasets are from Rotten Tomatoes, IMDB, TMD, Amazon and Roger Ebert. Source is collected by the creater of Magellan project.
* [WDC Product Data](http://webdatacommons.org/largescaleproductcorpus/v2/index.html): The source is collected by the authors of the project.