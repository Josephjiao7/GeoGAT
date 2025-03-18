# Geographical Graph Attention Networks
Geographical Graph Attention Networks: Spatial Deep Learning Models for Spatial Prediction and Exploratory Spatial Data Analysis

### Abstract
Some recent geospatial artificial intelligence (GeoAI) models have contributed to bridging the gap between artificial intelligence (AI) and spatial analysis. However, existing models struggle with handling small sample sizes for spatial prediction tasks across large areas. For exploratory spatial data analysis (ESDA), they are susceptible to distortion from local outliers and lack reliable interpretability methods that consider causal relationships. This study proposes Geographical Graph Attention Networks (GeoGATs), which are spatial deep learning models based on the principle of spatial (geographic) similarity. Two variants of the model are designed, namely GeoGAT-P for spatial prediction and GeoGAT-E for ESDA. Case studies using U.S. election data and homicide data demonstrate that GeoGAT-P can achieve more accurate predictions over a large spatial extent with a small-sample size than existing models. GeoGAT-E can achieve decent performance in comparison with existing models and understand complex spatial relationships. Our study demonstrates how spatial similarity can be integrated with the latest deep learning models, offering valuable insights for the future direction of GeoAI research.

### Spatial similarity in GeoGATs
According to [Zhu et al. (2018)](https://doi.org/10.1080/19475683.2018.1534890), spatial similarity refers to “the more similar the geographical configurations of two spatial units, the more similar the values of the target variable at these two spatial units”, and we use *S<sub>l</sub>* to express. 

It can consider not only the geographic configuration similarity between two spatial units but also the similarity in the composition and structure of geographic variables within the spatial neighborhoods surrounding these units. To this end, we further extend spatial similarity (*S<sub>l</sub>*) to incorporate the similarity of the neighborhoods of spatial units (*S<sub>n</sub>*), and use *S* to denote. 

<img src="https://github.com/user-attachments/assets/dd0ff9c7-c07a-4057-9e4b-000296b6ae3d" width="900">

### GeoGATs for prediction
We first calculate the spatial similarity (*S*) between a spatial observation and other observations, extracting the 10 most similar observations as neighboring nodes. Next, the spatial similarities are set as edge weights to help the model better understand spatial relationships. A masking operation ensures that each node only exchanges information and aggregates features with its neighboring nodes. In training process, dropout mask would randomly drop some parameters in GeoGAT-P to avoid overfitting. Finally, the model outputs the predicted values and generates a residual map.

<img src="https://github.com/user-attachments/assets/4404892e-a746-451b-a695-2b7ab75111af" width="900">

We compared the performance of Geographically Neural Network Weighted Regression (GNNWR), Spatial Regression Graph Convolutional Neural Network (SRGCNN), and GeoGAT-P models on the Elections dataset and the Homicides dataset. GeoGAT-P demonstrated the best predictive performance on both datasets.

To further understand GeoGAT-P, it is necessary to isolate the impact of spatial similarity on the GAT mechanism. We developed a baseline based on SRGCNN, referred to as SRGAT. In comparative tests, GeoGAT-P's superior spatial prediction performance primarily results from applying the spatial similarity principle rather than from the influence of the GAT mechanism.

Compared to GeoGAT-P*, which only considers the similarity between two observations (*S<sub>l</sub>*), GeoGAT-P enhances model robustness and predictive performance by integrating both the spatial similarity between observations and the similarity between their neighborhoods (*S*).

### GeoGATs for ESDA
Spatial data is the first input to identify neighboring nodes using Queen contiguity, Rook contiguity, K-Nearest Neighbors (KNN) or optimal bandwidth calculated by GWR, and then spatial similarity is calculated to determine the spatial similarity matrix (*S<sub>l</sub>*) as edge weights to establish a local model. Second, we design a causal attention mechanism and backdoor adjustment [(Sui et al., 2022)](https://dl.acm.org/doi/abs/10.1145/3534678.3539366) to deal with causal features and shortcut features. G represents graph-structured data; C are causal features, which are the predictors that truly affect the target feature y; S represents confounding variables, which are biases and noise in the data. Third, a masking operation facilitates information exchange and feature aggregation between nodes to train the model. Finally, the high-dimensional features extracted by the causal GAT layers are normalized and projected back to the original input feature space using linear layers to generate the map.

<img src="https://github.com/user-attachments/assets/942afcf5-f68e-41f9-bd93-bc8305ce625e" width="900">

Compared to Multiscale Geographically Weighted Regression (MGWR) and Geographical Random Forests (GRF), GeoGAT-E achieves the best performance on both datasets. In the causal attention mechanism, attention scores are used to measure the importance of each input feature's impact on the target feature. The higher the importance score, the stronger the relationship between that feature and the target feature.

In the following figures, the empirical analysis case of the Elections dataset indicates that White_pct has the largest global contribution to the model, followed by Female_pct and MTW_16, with HR contributing the least.

<img src="https://github.com/user-attachments/assets/4ab76507-81e2-4673-aca3-7ba7ab8f5d68" width="900">

<img src="https://github.com/user-attachments/assets/8b660109-1add-4602-a932-211fc66b19d6" width="900">

### Dataset
This study employed the public datasets of U.S. Elections and Homicides for empirical case studies, both of which were downloaded from [GeoDa Lab](https://geodacenter.github.io/data-and-lab/).

### Reference:
To cite this paper: Zhenzhi Jiao & Ran Tao (2025). Geographical Graph Attention Networks: Spatial Deep Learning Models for Spatial Prediction and Exploratory Spatial Data Analysis. Transactions in GIS. https://doi.org/10.1111/tgis.70029

Zhu, A. X., Lu, G., Liu, J., Qin, C. Z., & Zhou, C. (2018). Spatial prediction based on Third Law of Geography. Annals of GIS, 24(4), 225-240.

Sui, Y., Wang, X., Wu, J., Lin, M., He, X., & Chua, T. S. (2022, August). Causal attention for interpretable and generalizable graph classification. In Proceedings of the 28th ACM SIGKDD conference on knowledge discovery and data mining (pp. 1696-1705).


