# Geographical Graph Attention Networks
Geographical Graph Attention Networks: Spatial Deep Learning Models for Spatial Prediction and Exploratory Spatial Data Analysis

### Abstract
Some recent geospatial artificial intelligence (GeoAI) models have contributed to bridging the gap between artificial intelligence (AI) and spatial analysis. However, existing models struggle with handling small sample sizes for spatial prediction tasks across large areas. For exploratory spatial data analysis (ESDA), they are susceptible to distortion from local outliers and lack reliable interpretability methods that consider causal relationships. This study proposes Geographical Graph Attention Networks (GeoGATs), which are spatial deep learning models based on the principle of spatial (geographic) similarity. Two variants of the model are designed, namely GeoGAT-P for spatial prediction and GeoGAT-E for ESDA. Case studies using U.S. election data and homicide data demonstrate that GeoGAT-P can achieve more accurate predictions over a large spatial extent with a small-sample size than existing models. GeoGAT-E can achieve decent performance in comparison with existing models and understand complex spatial relationships. Our study demonstrates how spatial similarity can be integrated with the latest deep learning models, offering valuable insights for the future direction of GeoAI research.

### GeoGATs for prediction
As shown in the following figure, we first calculate the spatial similarity between a spatial observation and other observations, extracting the 10 most similar observations as neighboring nodes. Next, the spatial similarities are set as edge weights to help the model better understand spatial relationships. A masking operation ensures that each node only exchanges information and aggregates features with its neighboring nodes. In training process, dropout mask would randomly drop some parameters in GeoGAT-P to avoid overfitting. Finally, the model outputs the predicted values and generates a residual map.


### GeoGATs for ESDA
In the follwoing figure, spatial data is the first input to identify neighboring nodes using Queen contiguity, Rook contiguity, K-Nearest Neighbors (KNN) or optimal bandwidth calculated by GWR, and then spatial similarity is calculated to determine the spatial similarity matrix as edge weights to establish a local model. Second, we design a causal attention mechanism and backdoor adjustment to deal with causal features and shortcut features. G represents graph-structured data; C are causal features, which are the predictors that truly affect the target feature y; S represents confounding variables, which are biases and noise in the data. Third, a masking operation facilitates information exchange and feature aggregation between nodes to train the model. Finally, the high-dimensional features extracted by the graph convolution layers are normalized and projected back to the original input feature space using linear layers to generate the map.

### Spatial similarity in GeoGATs
According to [Zhu et al. (2018)](https://doi.org/10.1080/19475683.2018.1534890), spatial similarity can consider not only the geographic configuration similarity between two spatial units but also the similarity in the composition and structure of geographic variables within the spatial neighborhoods surrounding these units. To this end, we further extend spatial similarity to incorporate the similarity of the neighborhoods of spatial units.

### Dataset
This study use the public datasets of U.S. Elections and Homicides for empirical case studies, both of which were downloaded from [GeoDa Lab](https://geodacenter.github.io/data-and-lab/).

### Reference:
To cite this paper: Zhenzhi Jiao & Ran Tao (2025). Geographical Graph Attention Networks: Spatial Deep Learning Models for Spatial Prediction and Exploratory Spatial Data Analysis. Transactions in GIS. (Accepted)

Zhu, A. X., Lu, G., Liu, J., Qin, C. Z., & Zhou, C. (2018). Spatial prediction based on Third Law of Geography. Annals of GIS, 24(4), 225-240.

Sui, Y., Wang, X., Wu, J., Lin, M., He, X., & Chua, T. S. (2022, August). Causal attention for interpretable and generalizable graph classification. In Proceedings of the 28th ACM SIGKDD conference on knowledge discovery and data mining (pp. 1696-1705).


