# The PersonX Dataset

![Fig 1](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/logo1.jpg)

Visual factors such as viewpoint, pose, illumination and background, are usually condisered as important challenges in person re-identification (re-ID). However, despite the acknowledgement that these factors are influential, quantitative studies on how they affect a re-ID system are still lacking. To derive insights in this scientific campaign, the burning problem needed to be settled is collecting quantitative data. However, it is difficult to control the changes of visual factors in practice and the cost of collecting this kind of data is expensive. To solve this problem, we build a synthetic data engine [PersonX](https://github.com/sxzrt/Instructions-of-the-PersonX-dataset).


## 1. Dataset introduction 
The PersonX dataset contains six backgrounds, including three pure color backgrounds and three scene backgrounds. There are 1266 hand-crafted identities (547 females and 719 males) and each identety has 36 images (corresponding to 36 viewpoints that are defined below). In this work, we combine two different backgrounds as one dataset to study different situations. The backgrounds and subsets of PersonX are shows as follows.

![Fig 2](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/fig2.jpg)

## 2. Dataset validation 
To show the feasible of using sunthetic data, we conduct experiments on both real-world (the Market-1501/1203 and Duke datasets)and synthetic datasets by using evaluate three algorithms IDE+, triplet feature and PCB. The results are shown in the follwing figure.

<div align=center><img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/benchmark.jpg" width="800" /></div>

    `“lr” means the frames are low resolution of 512×242 instead of the original resolution 1024×768`

Three characteristics of PersonX can be observed from the validaton results:
* **Eligibility:** the performance trend of the three algorithms is similar between PersonX and real-world datasets
* **Purity:** the re-ID accuracies on PersonX subsets are relatively high compared to the real-world dataset
* **Sensitivity:** these subsets are sensitive to the changes in the environment, such as changes of resolution.


****

# Dissecting Person Re-identification from the Viewpoint of Viewpoint 
Based on the PersonX engine, this paper makes an early attempt in studying a particular factor, **viewpoint**.

![Fig 4](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/fig-dfv.jpg)

Here, we denote viewpoint as the pedestrian rotation angle (as shown in above Figure). Since different views of a person contain different details, the viewpoint of a person influences the visual information contained in the image, which is directly related to the performance of the algorithm. Therefore, we investigate the exact influence of viewpoint on the system from **three** aspects. 


## 1. How do viewpoint distributions in the training set affect model learning?
### 1.1 Experiment design
* Control group 1. We randomly select half (18 out of 36) or a quarter (9 out of 36) images of each identity
for training.
* Control group 2. The training set is constituted by randomly selecting half (18 out of 36) or a quarter (9 out of 36) viewpoints for each identity.
There is an example of Control group 1 and Control group2 in the follwing figure.

<div align="center">
  <img src="https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/v3-valse1.jpg" width="600">
</div>

* Experimental group 1. Train with two orientations. The training images exhibit two orientations, left+right or front+back. The training set is thus half of the original training set.
* Experimental group 2. Train with one orientation. The training set has one orientation, i.e., left, right, front, or back. The training set becomes a quarter of the size of the original training set.

### 1.2 Experiment results
The Re-ID accuracy (mAP, %) when the training set has missing orientations/viewpoints is shown in following figure.

![Fig 6](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/Train-1.jpg)

Here, **A** and **B**: we use two orientations for training. For example, we can train with left and right orientations only (see the  definition of viewpoint). **C**: we train with one orientation only, *i.e.,* left, right, front, or back orientation. For each dataset, we have two control groups. **D**: Impact of missing continuous viewpoints on PersonX46. The horizontal axis is the remaining number of viewpoints and vertical axis is the mAP. In the experimental group, continuous viewpoints are removed. The number on this curve denotes the remaining number of viewpoints.
“n.s.” represents that the difference between results is not statistically significant (i.e., p-value > 0.05).  ★ corresponds to statistically significant (*i.e.,* 0.01 < p-value < 0.05). ★★★ means the difference between results is statistically very significant (*i.e.,* 0.001 < p-value < 0.01).

### 1.3 Subsection conclusions
* Missing viewpoints compromises training.
* Missing continuous viewpoints are more detrimental than missing randomly viewpoints.
* When limited training viewpoints are available, left/right orientations allow models to be better trained than front/back orientations.


## 2. How do true match viewpoints in the gallery affect retrieval?
### 1.1 Experiment design
### 1.2 Experiment results
### 1.3 Subsection conclusions
## 3. How does the query viewpoint influence the retrieval?



