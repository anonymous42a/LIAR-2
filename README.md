# LIAR 2

The [LIAR](https://doi.org/10.18653/v1/P17-2067) dataset has been widely followed by fake news detection researchers since its release, and along with a great deal of research, the community has provided a variety of feedback on the dataset to improve it. We adopted these feedbacks and released the LIAR 2 dataset, a new benchmark dataset of ~23k manually labeled by professional fact-checkers for fake news detection tasks. We have used a split ratio of 8:1:1 to distinguish between the training set, the test set, and the validation set, details of which are provided in the following table. The LIAR 2 dataset can be accessed at [`./LIAR2`]()

| **Statistics**                               | **LIAR** | **LIAR 2** |
|----------------------------------------------|----------|------------|
| Training set size                            | 10,269   | 18,369     |
| Validation set size                          | 1,284    | 2,297      |
| Testing set size                             | 1,283    | 2,296      |
| Avg. statement length (tokens)               | 17.9     | 17.7       |
| Avg. speaker description length (tokens)     | \        | 39.4       |
| Avg. justification length (tokens)           | \        | 94.4       |
| **Labels**
| Pants on fire                                | 1,050    | 3,031      |
| False                                        | 2,511    | 6,605      |
| Barely-true                                  | 2,108    | 3,603      |
| Half-true                                    | 2,638    | 3,709      |
| Mostly-true                                  | 2,466    | 3,429      |
| True                                         | 2,063    | 2,585      |

## Dataset Features

Here is the information and meaning of the dataset features:

| **Field** | **Type** | **Description** |
| --- | --- | --- |
| id | int | The unique identifier of each statement. |
| label | int | The 6-grade truthfulness label for each statement. |
| statement | string | The entity of the statement. |
| date | string | Date of announcement of the statement. |
| subject | string | The subject to which the claim relates. |
| speaker | string | Speaker of the statement. |
| speaker\_description | string | Biography and description of speaker. |
| state\_info| string | The state information to which the statement relates. |
| true\_counts | int | Credibility history (true) of the speaker. |
| mostly\_true_counts | int | Credibility history (mostly-true) of the speaker. |
| half\_true\_counts | int | Credibility history (half-true) of the speaker. |
| mostly_false_counts | int | Credibility history (mostly-false) of the speaker. |
| false_counts | int | Credibility history (false) of the speaker. |
| pants_on_fire_counts | int | Credibility history (pants-on-fire) of the speaker. |
| context | string | The venue or location where the statement was announced. |
| justification | string | Justification for the fact-checking decision. |

## Example

This is an example of a random take from the LIAR 2 dataset.

| **Field** | **Value** |
| --- | --- |
| id | 23033 |
| label | 2 |
| statement | The Republican plan would cut federal law enfo... |
| date | May 10, 2023 |
| subject | immigration;federal budget;public safety |
| speaker | joe biden |
| speaker\_description | Joe Biden is the president of the United State... |
| state\_info| national |
| true\_counts | 25 |
| mostly\_true_counts | 64 |
| half\_true\_counts | 65 |
| mostly_false_counts | 52 |
| false_counts | 55 |
| pants_on_fire_counts | 7 |
| context | New York |
| justification | Biden said, "The Republican plan would cut fed... |

## Comparison Experiments with the Original LIAR Dataset
we conducted a total of five groups of experiments and the results are presented in the following table. To make the comparison easy, we split the LIAR 2 dataset into two parts: $LIAR\ 2 = LIAR + NEW$. LIAR refers to the original LIAR dataset after we enhance the structure, and NEW denotes the data that we expand on the original LIAR dataset, i.e., the incremental part.

Performance metrics for experiments on the split LIAR 2 dataset. Numbers in parentheses indicate the proportion of the segment that is split. Original in the first line means the unmodified official version of the LIAR dataset, while without original it is the LIAR dataset that has been structured by our enhancement. The mix marking in the last line means that the LIAR and NEW parts are all mixed together before splitting, i.e., experiments on the full LIAR 2 dataset. All results were obtained by using the FDHN model, as the FDHN model has been validated to achieve current state-of-the-art performance on the LIAR dataset, and experimental code and records on FDHN on the LIAR dataset are provided in the [`./FDHN`](). All source code and records related to this comparison experiment can be accessed under [`./dataset_comparison`](/dataset_comparison).


| **Train**              | **Test & Val.**       | **Val. Accuracy** | **Val. F1-Macro** | **Val. F1-Micro** | **Test Accuracy** | **Test F1-Macro** | **Test F1-Micro** | **Mean** |
|------------------------|------------------------|--------------------------|-------------------------|-------------------------|-------------------|------------------|------------------|----------|
| LIAR (Original .8)      | LIAR (Original .2)     | 0.4673                   | 0.4490                  | 0.4577                  | 0.4649            | 0.4701           | 0.4649           | 0.4623   |
| LIAR (.8)               | LIAR (.2)              | 0.6140                   | 0.5888                  | 0.5833                  | 0.6084            | 0.6138           | 0.6084           | 0.6028   |
| NEW (.8)                | NEW (.2)               | 0.7676                   | 0.6706                  | 0.7473                  | 0.7592            | 0.6952           | 0.7592           | 0.7332   |
| LIAR (1.)               | NEW (1.)               | 0.7361                   | 0.6963                  | 0.7301                  | 0.7361            | 0.7057           | 0.7361           | 0.7234   |
| NEW (1.)                | LIAR (1.)              | 0.5575                   | 0.5203                  | 0.5199                  | 0.5575            | 0.5626           | 0.5575           | 0.5459   |
| LIAR (1.) + NEW (.557)  | NEW (.443)             | 0.7867                   | 0.7249                  | 0.7696                  | 0.7827            | 0.7389           | 0.7827           | 0.7643   |
| LIAR (.635) + NEW (1.) | LIAR (.365)            | 0.6308                   | 0.6118                  | 0.6073                  | 0.6211            | 0.6270           | 0.6211           | 0.6199   |
| LIAR (.8) + NEW (.8)    | LIAR (.2) + NEW (.2)   | 0.6977                   | 0.6671                  | 0.6771                  | 0.6892            | 0.6828           | 0.6892           | 0.6839   |
| LIAR + NEW (Mix .8)     | LIAR + NEW (Mix .2)    | 0.6974                   | 0.6570                  | 0.6676                  | 0.7021            | 0.6961           | 0.7021           | 0.6871   |


## Ablation Experiment

The LIAR 2 dataset is an upgrade of the LIAR dataset, which inherits the ideas of the LIAR dataset, refines the details and architecture, and expands the size of the dataset to make it more responsive to the needs of fake news detection tasks. We believe that with the help of the LIAR 2 dataset, it will be able to perform better fake news detection tasks. The analysis and baseline information about the LIAR 2 dataset is provided in below. All source code and records related to this ablation experiment can be accessed under [`./dataset_ablation`](/dataset_ablation).

| **Feature**              | **Val. Accuracy** | **Val. F1-Macro** | **Val. F1-Micro** | **Test Accuracy** | **Test F1-Macro** | **Test F1-Micro** | **Mean** |
|--------------------------|-------------------|-------------------|-------------------|-------------------|-------------------|-------------------|----------|
| Statement              | 0.3174       | 0.1957       | 0.3117       | 0.3197       | 0.2380       | 0.3197       | 0.2837 |
| Date                   | 0.2912       | 0.1879       | 0.2912       | 0.3079       | 0.1775       | 0.3079       | 0.2606 |
| Subject                | 0.3243       | 0.2311       | 0.3183       | 0.3267       | 0.2271       | 0.3267       | 0.2924 |
| Speaker                | 0.3283       | 0.2250       | 0.3174       | 0.3310       | 0.2462       | 0.3310       | 0.2965 |
| Speaker Description    | 0.3322       | 0.2444       | 0.3250       | 0.3280       | 0.2444       | 0.3280       | 0.3003 |
| State Info             | 0.2930       | 0.1577       | 0.2950       | 0.2979       | 0.1521       | 0.2979       | 0.2489 |
| Credibility History    | 0.5007       | 0.4696       | 0.4985       | 0.5057       | 0.4656       | 0.5057       | 0.4910 |
| Context                | 0.2982       | 0.1817       | 0.2982       | 0.3132       | 0.1791       | 0.3132       | 0.2639 |
| Justification          | **0.5964**   | **0.5657**   | **0.5827**   | **0.6115**   | **0.5968**   | **0.6115**   | **0.5941** |
| All without 
|Statement               | **0.7079**   | **0.6734**   | **0.6822**   | **0.7182**   | **0.7108**   | **0.7182**   | **0.7018** |
| Date                   | 0.6931       | 0.6572       | 0.6680       | 0.7078       | 0.6993       | 0.7078       | 0.6889 |
| Subject                | 0.7000       | 0.6579       | 0.6681       | 0.7078       | 0.7013       | 0.7078       | 0.6905 |
| Speaker                | 0.6944       | 0.6648       | 0.6757       | 0.7043       | 0.6942       | 0.7043       | 0.6896 |
| Speaker Description    | 0.6892       | 0.6640       | 0.6739       | 0.7169       | 0.7073       | 0.7169       | 0.6947 |
| State Info             | 0.7074       | 0.6625       | 0.6729       | 0.7099       | 0.7016       | 0.7099       | 0.6940 |
| Credibility History    | 0.6025       | 0.5717       | 0.5900       | 0.6185       | 0.6046       | 0.6185       | 0.6010 |
| Context                | 0.7005       | 0.6622       | 0.6720       | 0.7043       | 0.6967       | 0.7043       | 0.6900 |
| Justification          | 0.5285       | 0.4898       | 0.5153       | 0.5340       | 0.5148       | 0.5340       | 0.5194 |
| Statement +
| Date                   | 0.3431       | 0.2540       | 0.3343       | 0.3380       | 0.2514       | 0.3380       | 0.3098 |
| Subject                | 0.3548       | 0.2759       | 0.3513       | 0.3375       | 0.2580       | 0.3375       | 0.3192 |
| Speaker                | 0.3618       | 0.2862       | 0.3539       | 0.3476       | 0.2640       | 0.3476       | 0.3269 |
| Speaker Description    | 0.3583       | 0.2814       | 0.3531       | 0.3667       | 0.2886       | 0.3667       | 0.3358 |
| State Info             | 0.3317       | 0.2367       | 0.3294       | 0.3328       | 0.2362       | 0.3328       | 0.2999 |
| Credibility History    | 0.5067       | 0.4737       | 0.5084       | 0.5244       | 0.5000       | 0.5244       | 0.5063 |
| Context                | 0.3361       | 0.2682       | 0.3391       | 0.3458       | 0.2560       | 0.3458       | 0.3152 |
| Justification          | 0.6017       | 0.5578       | 0.5796       | 0.6176       | 0.6026       | 0.6176       | 0.5962 |
| All                    | **0.6974**   | **0.6570**   | **0.6676**   | **0.7021**   | **0.6961**   | **0.7021**   | **0.6871**|

## Citation

If you find our work useful in your research, please consider citing:

```bibtex
@inproceedings{Anonymous2023,
   title = {XXX},
   author = {Anonymous},
   booktitle = {Proceedings of the Anonymous Conference},
   year = {2023}
}
