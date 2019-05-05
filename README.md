# The PersonX Dataset

![Fig 1](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/logo1.jpg)

Visual factors such as viewpoint, pose, illumination and background, are usually considered as important challenges in person re-identification (re-ID). Despite the acknowledgement that these factors are influential, quantitative studies on how they affect a re-ID system are still lacking. To derive insights in this scientific campaign, the burning problem needed to be settled is collecting quantitative data. However, it is difficult to control the changes of visual factors in practice and the cost of collecting this kind of data is expensive. Therefore, we build a synthetic data engine [PersonX](https://github.com/sxzrt/Instructions-of-the-PersonX-dataset) (the [link](https://arxiv.org/pdf/1812.02162.pdf) of paper).
## List of contents
* [1. Dataset introduction](#1-dataset-introduction)
* [2. Dataset validation](#2-dataset-validation)
* [3. Dissecting Person Re-identification from the Viewpoint of Viewpoint](#3-dissecting-person-re-identification-from-the-viewpoint-of-viewpoint)
    * [3.1. How do viewpoint distributions in the training set affect model learning?](#31-how-do-viewpoint-distributions-in-the-training-set-affect-model-learning)
    * [3.2. How do true match viewpoints in the gallery affect retrieval?](#32-how-do-true-match-viewpoints-in-the-gallery-affect-retrieval)
    * [3.3. How does the query viewpoint influence the retrieval?](#33-how-does-the-query-viewpoint-influence-the-retrieval)

## 1. Dataset introduction 
The PersonX dataset contains six backgrounds, including three pure color backgrounds and three scene backgrounds. There are 1266 hand-crafted identities (547 females and 719 males) and each identity has 36 images (corresponding to 36 viewpoints that are defined below). In this work, we combine two different backgrounds as one dataset to study different situations. The backgrounds and subsets of PersonX are shows as follows.

![Fig 2](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/fig2.jpg)

## 2. Dataset validation 
To show the feasible of using synthetic data, we conduct experiments on both real-world (the Market-1501/1203 and Duke datasets) and synthetic datasets by using evaluate three algorithms IDE+, triplet feature and PCB. The results are shown in the following figure.

<div align=center><img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/benchmark.jpg" width="800" /></div>

    `“lr” means the frames are low resolution of 512×242 instead of the original resolution 1024×768`

Three characteristics of PersonX can be observed from the validation results:
* **Eligibility:** the performance trend of the three algorithms is similar between PersonX and real-world datasets
* **Purity:** the re-ID accuracies on PersonX subsets are relatively high compared to the real-world dataset
* **Sensitivity:** these subsets are sensitive to the changes in the environment, such as changes of resolution.


****

## 3. Dissecting Person Re-identification from the Viewpoint of Viewpoint 
Based on the PersonX engine, this paper makes an early attempt in studying a particular factor, **viewpoint**.

![Fig 4](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/fig-dfv.jpg)

Here, we denote viewpoint as the pedestrian rotation angle (as shown in above Figure). Since different views of a person contain different details, the viewpoint of a person influences the visual information contained in the image, which is directly related to the performance of the algorithm. Therefore, we investigate the exact influence of viewpoint on the system from **three** aspects. 


## 3.1. How do viewpoint distributions in the training set affect model learning
### 3.1.1 Experiment design
* Control group 1. We randomly select half (18 out of 36) or a quarter (9 out of 36) images of each identity
for training.
* Control group 2. The training set is constituted by randomly selecting half (18 out of 36) or a quarter (9 out of 36) viewpoints for each identity.
There is an example of Control group 1 and Control group2 in the following figure.

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/v3-valse1.jpg" width="600">
</div>

* Experimental group 1. Train with two orientations. The training images exhibit two orientations, left+right or front+back. The training set is thus half of the original training set.
* Experimental group 2. Train with one orientation. The training set has one orientation, i.e., left, right, front, or back. The training set becomes a quarter of the size of the original training set.

### 3.1.2 Experiment results
The Re-ID accuracy (mAP, %) when the training set has missing orientations/viewpoints is shown in following figure.

![Fig 6](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/Train-1.jpg)

Here, **A** and **B**: we use two orientations for training. For example, we can train with left and right orientations only (see the definition of viewpoint). **C**: we train with one orientation only, *i.e.,* left, right, front, or back orientation. For each dataset, we have two control groups. **D**: Impact of missing continuous viewpoints on PersonX46. The horizontal axis is the remaining number of viewpoints and vertical axis is the mAP. In the experimental group, continuous viewpoints are removed. The number on this curve denotes the remaining number of viewpoints.
“n.s.” represents that the difference between results is not statistically significant (i.e., p-value > 0.05).  ★ corresponds to statistically significant (*i.e.,* 0.01 < p-value < 0.05). ★★★ means the difference between results is statistically very significant (*i.e.,* 0.001 < p-value < 0.01).

### 3.1.3 Subsection conclusions
* Missing viewpoints compromises training.
* Missing continuous viewpoints are more detrimental than missing randomly viewpoints.
* When limited training viewpoints are available, left/right orientations allow models to be better trained than front/back orientations.


## 3.2. How do true match viewpoints in the gallery affect retrieval
### 3.2.1 Experiment design
We denote the viewpoint of a query and its true match as <a href="https://www.codecogs.com/eqnedit.php?latex=\theta_{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta_{t}" title="\theta_{t}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\theta_{q}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta_{q}" title="\theta_{q}" /></a>, respectively.
* Experimental group 1. The three true matches whose <a href="https://www.codecogs.com/eqnedit.php?latex=\theta_{t}&space;\in&space;\theta_{q}\pm&space;10^o" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta_{t}&space;\in&space;\theta_{q}\pm&space;10^o" title="\theta_{t} \in \theta_{q}\pm 10^o" /></a> are removed (set as “junk”).
* Control group 1. Three true matches are randomly removed from the gallery. The illustrations are shown as follows:  

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/ed2.jpg" width="600">
</div>

Similarly, experimental group 2 and 3, as well as control group 2 and 3 means remove Five (<a href="https://www.codecogs.com/eqnedit.php?latex=\theta_{t}&space;\in&space;\theta_{q}\pm&space;10^o" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta_{t}&space;\in&space;\theta_{q}\pm&space;20^o" title="\theta_{t} \in \theta_{q}\pm 20^o" /></a>) and Nine (<a href="https://www.codecogs.com/eqnedit.php?latex=\theta_{t}&space;\in&space;\theta_{q}\pm&space;10^o" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta_{t}&space;\in&space;\theta_{q}\pm&space;40^o" title="\theta_{t} \in \theta_{q}\pm 40^o" /></a>)  images, respectively.

### 3.2.2 Experiment results
Experiments are conducted on PersonX45, PersonX46, PersonX46-lr as well as Market-1203. 

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/gallery.jpg" width="600">
</div>

### 3.2.3 Subsection conclusions
* True matches whose viewpoints are dissimilar to the query are harder to be retrieved than true matches with a similar viewpoint to the query.
* The above problem becomes more severe when the environment is challenging, *e.g.,* complex background and low resolution.


## 3.3. How does the query viewpoint influence the retrieval?
### 3.3.1 Experiment design
We train a model on the original training set comprised of every viewpoint. We modify the query viewpoints to see its effect during testing. Specifically, the viewpoint of a probe image can be set to the **due left (0)**, **due front (90)**, **due right (180)** or **due back (270)** to represent different sides of person. During retrieval, we assume only one true match in gallery; the true
match contains the same person as the query, and its viewpoint is between 0 and 350. Viewpoints of the distractor gallery images are images of all other persons. Taking using due left as query viewpoint as an example, the setting is shown as follows: 

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/ed3.jpg" width="700">
</div>

### 3.3.2 Experiment results
For four kinds of query viewpoints, the results are shown in below figure.

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/test1.jpg" width="400">
</div>

Under each query viewpoint, we report 36 rank-1 scores obtained by the query to retrieve 36 types of true match viewpoints. The mean value of 36 rank-1 scores of each kind of query viewpoint is also reported.

### 3.3.3 Subsection conclusions

* The query viewpoint of left/right generally leads to higher re-ID accuracy than front/back viewpoints.



**** 
If you use this dataset in your research, please kindly cite our work as, <br>
```
@inproceedings{sun2019dissecting,
	title={Dissecting Person Re-identification from the Viewpoint of Viewpoint},
	author={Sun, Xiaoxiao and Zheng, Liang},
	booktitle={CVPR},
	year={2019}
}
```
