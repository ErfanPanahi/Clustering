# Clustering
This repository deals with the implementation of the K-Means clustering algorithm. Subsequently, the intelligent K-Means clustering algorithm is utilized for Constrained Clustering.

**Problem 1.** Analytical

In this section, we focus on the examination and manual resolution of clustering algorithms.

***Part A:*** Clustering Using K-Means Method

Using the k-means clustering method, first, we calculate the squared distance matrix of the following data points, and then we divide them into two clusters.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/9df7af0c-21e4-41be-8b23-b587d98d47db)

The distance between two points $x_i$ and $x_j$:

$D_{ij}=dist_{eucl.} (x_i,x_j)^2=(x_{i,1}-x_{j,1})^2+(x_{i,2}-x_{j,2})^2$

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/bc10ad8a-663d-43f1-9616-c9ca6b1f7ca6)

***Part B:*** Hierarchical Clustering

**Single Linkage:** In this method, we start by considering the smallest distance and initiate the clustering. At each step, we select the smallest distance between each data point and a cluster, update the distance table, and determine the clustering boundary.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/ac62095c-e9cc-4488-89ed-7fe57243be6a)

**Complete Linkage:** In this method, we start with the smallest distance and initiate the clustering. In each step, we select the maximum distance of each data point with a cluster, then update the distance table and determine the cluster boundary.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/a1f24291-4bfa-4efb-94c8-61aff8471136)

**Comparison:** In this section, we intend to modify two values from the distance matrix in a way that the final tree of the Complete Linkage algorithm becomes similar to the final tree of the Single Linkage algorithm. Accordingly, we proceed through the stages of the Complete Linkage until the clusters resemble those of the Single Linkage. Whenever a difference between the two algorithms is observed, we adjust a value in the matrix to align the outputs of the two algorithms.

**Problem 2.** Implementation of Clustering Algorithm

***Part 1:*** Simple K-Means Clustering

In this question, we focus on implementing the K-Means clustering algorithm. The goal of this unsupervised algorithm is to minimize the cost function J, which is defined as the sum of distances between instances belonging to each cluster and the center of that cluster (intra-class distance).

With the consideration of the Iris dataset, we aim to implement the k-means clustering algorithm using the Euclidean norm.

    from sklearn.datasets import load_iris
    data = load_iris()

To implement this algorithm, we first randomly select k data points and consider them as cluster centers. Then, in an iterative loop, we run the k-Means algorithm. To do this, each time we calculate the distance matrix of data points from the cluster centers and perform clustering based on the minimum distance to the cluster centers. Subsequently, we obtain new cluster centers by taking the average of the data points within each cluster. In the function written for this section, the input "ITR" signifies that if we want to repeat the algorithm for a specific number of iterations, we assign that desired value. Otherwise, when the optimal centers are calculated, the algorithm terminates.

***A:*** The Impact of the Number of Clusters

In this section, to compare the effect of the number of clusters in the k-Means algorithm, we plot the cost function value for each desired value of k. The image below depicts the change in the cost function value for k values of {5, 10, 20}.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/eab1fd9b-5bf7-4ec4-a66f-29cd83b77617)

As observed in these images, the algorithm converges after around 5 iterations for each k value. Additionally, the image below presents a comparison of the three graphs in one plot. As seen in this image, the cost function value has decreased for larger k values. This is natural since increasing the number of clusters reduces the distance between data points and the centers. However, it's important to note that this does not necessarily imply that the algorithm performs better for larger k values.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/54c45a68-7789-4f92-88ff-0d3a17d3cc2b)

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/e4da22f9-0d58-4608-bb86-8b70c9190ace)

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/2dbc9ca1-298b-4614-8abf-3fb4a1bc89f0)

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/21c498ce-03c6-48f4-ae7d-3f15643d3de0)

***Part 2:*** Intelligent k-Means Clustering

In this section, following the instructions provided in the exercise, we aim to perform clustering in a way that satisfies the given conditions. Now we want to explain the algorithm that leads to meeting these conditions and implement it.

**Section A:** Algorithm Design and Implementation

The algorithm discussed in this section will be similar to the k-means algorithm overall, with the difference that we stop at the end of each iteration and check each condition. 

Initially, based on the desired number of conditions, we randomly select conditions from the given set. During the stopping and condition-checking phase, we examine one condition at a time. We know that conditions have two states. If two given indices are in the same cluster, the state is 1, and if they are not in the same cluster, the state is -1. Therefore, we examine each state separately and ensure that the conditions are satisfied for clustering in the end. 

**State 1:** In this state, we check whether the two given indices are in the same cluster or not. If they are not in the same cluster, we cluster them together as follows:

If we name the cluster related to index 1 (ind1) as cluster1 and the cluster related to index 2 (ind2) as cluster2, there are two ways to cluster the two indices. One way is to assign ind2 to cluster1, and the other way is to assign ind1 to cluster2. To determine which way is better, we calculate the cost function, which is the sum of distances to the centroids, for each case and choose the one with lower cost. This way, the two indices are clustered together.

cost1 = dist(ind1, cluster1) + dist(ind2, cluster1)
cost2 = dist(ind1, cluster2) + dist(ind2, cluster2)

**State 2:** In this state, we check whether the two given indices are in different clusters or not. If they are in the same cluster, we differentiate their clusters as follows:

First, we try to find the second nearest cluster center to each index. If we name the cluster of the two indices as cluster0, the second nearest cluster of index 1 (ind1) as cluster1, and the second nearest cluster of index 2 (ind2) as cluster2, there are two ways to assign the two indices to different clusters. One way is to assign ind2 to cluster2, and the other way is to assign ind1 to cluster1. To determine which way is better, we calculate the cost function, which is the sum of distances to the centroids, for each case and choose the one with lower cost. This way, the two indices are clustered in different clusters.

cost1 = dist(ind1, cluster0) + dist(ind2, cluster2)
cost2 = dist(ind1, cluster1) + dist(ind2, cluster0)

We execute this algorithm for all conditions. The "Constraints_Check()" function is written to check and satisfy the conditions.

**Section B:** Algorithm Evaluation

***Problem 1:*** In this section, for k values of {3, 5, 10, 20} and size_cons values of {20, 40, 60}, we compare clustering. To do this, we consider the evaluation criterion as the average of the Ratio and Cost functions for 10 iterations and plot the corresponding graphs for each case. The image below illustrates the graphs of the average Ratio and Cost functions against k for different numbers of conditions.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/811d9951-203b-4b75-a1b3-dd45dba0dca2)

***Problem 2:*** Now, for k=3, we want to compare the accuracy of clustering for the simple and intelligent clustering algorithms with the required number of conditions. Given that we have Labels for the data, where the first, second, and third sets of 50 data points each belong to one cluster, we obtain the clustering accuracy. (Note that the cluster numbers do not necessarily match the Label data, so we calculate the maximum repetition within each set of 50 data points and calculate the overall accuracy. As expected, as shown in the accompanying figure, the accuracy of intelligent clustering is higher compared to simple clustering, and as we increase the number of conditions, this accuracy also increases.

![image](https://github.com/ErfanPanahi/Clustering/assets/107314081/fd4cc665-de0a-4e0c-9093-18b5c4a066d1)
