## The PersonX Dataset

![](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/logo1.jpg)

Visual factors such as viewpoint, pose, illumination and background, are usually condisered as important challenges in person re-identification (re-ID). However, despite the acknowledgement that these factors are influential, quantitative studies on how they affect a re-ID system are still lacking. To derive insights in this scientific campaign, the burning problem needed to be settled is collecting quantitative data. However, it is difficult to control the changes of visual factors in practice and the cost of collecting this kind of data is expensive. To solve this problem, we build a synthetic data engine [PersonX](https://github.com/sxzrt/Instructions-of-the-PersonX-dataset).

****

## Dissecting Person Re-identification from the Viewpoint of Viewpoint 
Based on the PersonX engine, this paper makes an early attempt in studying a particular factor, **viewpoint**.
![](https://github.com/sxzrt/The-PersonX-dataset/blob/master/images/fig-dfv.jpg)

Here, we denote viewpoint as the pedestrian rotation angle (as shown in above Figure). Since different views of a person contain different details, the viewpoint of a person influences the visual information contained in the image, which is directly related to the performance of the algorithm. Therefore, we investigate the exact influence of viewpoint on the system from **three** aspects. 


### 1. How do viewpoint distributions in the training set affect model learning?



### 2. How do true match viewpoints in the gallery affect retrieval?

### 3. How does the query viewpoint influence the retrieval?



