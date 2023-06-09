# Content-Based Image Retrieval using the FoodX-251 dataset

***Part of the Visual Information Processing and Management project | UniMiB***

The purpose of the project is to compare three different methods for retrieving the best 5 similar images given a query one.

<img src="Images/query_example.jpg" width=640>

Main differences between the proposed methods:

### 1. Transfer learning from a pre-trained CNN

- Extraction feature from the first dense layer of MobileNet v2 (1x1280);
- cosine similarity as similarity measure;
- for-loop structure to check all possible combinations of pairs of images;
- tentative use of KDTree to reduce the complexity of the searching algorithm (from O(n) to O(logn)) but lower performance.

<img src="Images/cnn_architecture.jpg" width=320 height=120>

### 2. BoWA (Bag of Words using AKAZE descriptors)

- Identification of the most relevant keypoint of each image using 0.01 as threshold for AKZE descriptors
- application of the K-means clustering algorithm to detect centroids (K = 251);
- representation of each image according to the obtained centroids (BOW approach);
- KNN as similarity measure.

<img src="Images/akaze_example.jpg" width=320 height=120>

Reference: *Muhammad, Usman, et al., "Bag of Words KAZE (BoWK) with two‐step classification for high‐resolution remote sensing images." IET Computer Vision 13.4 (2019): 395-403.*

### 3. Siamese network trained using triplet loss as feature extractor

- Definition of embedding model and replication of it using triplet loss;
- each triplet is composed of an Anchor, a Positive example and a Negative one;
- use of the trained NN as feature extractor;
- KNN as similarity measure.

<img src="Images/triplet_example.jpg" width=320 height=120>

## Results

The table below contains the performance of the methods described according to the top-5 accuracy metric. 

| Approach        | Top-5 accuracy | 
| --------------- | -------------- | 
| CNN             | ***31%***      | 
| CNN with KDTree | 24%            |
| BoWA            | 7%             |
| Siamese network | 15%            |

As shown in the table, the method that uses transfer learning from a pre-trained CNN obtains the best result. 

*Note:* It is important to underline that during the analysis, some images that are not correctly labeled have emerged; an initial data cleaning step on the original dataset is required to not misleal further analysis.
