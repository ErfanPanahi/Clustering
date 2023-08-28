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


