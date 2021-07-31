# project title
## Capacitated clustering problem
In a capacitated clustering problem (CCP) set of n items having some weights/demands are grouped/clustered into k clusters which are all disjoint such that the total weight of a cluster does not cross the maximum capacity. Here we assume that all the individual weights/demands are less than the max. capacity and capacity for all clusters is same.

Example of a CCP is a Vehicle Routing Problem (VRP) with one depot and multiple vehicles of same capacity. There are n cities each with some demand and the problem is to travel in such a way that their demand is satisfied and we get to travel only the minimum distance.

So the solution of a VRP can be understood as a task of clustering the cities in such a way that max. capacity constraint is satisfied and distance travelled is minimum.

## K-means algorithm
K-means algorithm is a famous unsupervised machine learning algorithm used for classification when the no. of classes is known.
Kmeans algorithm is an iterative algorithm that tries to partition the dataset into Kpre-defined distinct non-overlapping subgroups (clusters) where each data point belongs to only one group. It tries to make the intra-cluster data points as similar as possible while also keeping the clusters as different (far) as possible. It assigns data points to a cluster such that the sum of the squared distance between the data points and the cluster’s centroid (arithmetic mean of all the data points that belong to that cluster) is at the minimum. The less variation we have within clusters, the more homogeneous (similar) the data points are within the same cluster.

The way kmeans algorithm works is as follows:

    1. Specify number of clusters K.
    2. Initialize centroids by first shuffling the dataset and then randomly selecting K data points for the centroids without replacement.
    3. Keep iterating until there is no change to the centroids. i.e assignment of data points to clusters isn’t changing.

    4. Compute the sum of the squared distance between data points and all centroids.
    5. Assign each data point to the closest cluster (centroid).
    6. Compute the centroids for the clusters by taking the average of the all data points that belong to each cluster.
    
The approach kmeans follows to solve the problem is called Expectation-Maximization. The E-step is assigning the data points to the closest cluster. The M-step is computing the centroid of each cluster.

The objective function is:

![](https://github.com/kshitij-pro/capacitated_clustering/blob/8c4e44e4a10c9c72108083d5df20e80340a2ffdc/Screenshot%202021-07-31%20172759.png)

where wik=1 for data point xi if it belongs to cluster k; otherwise, wik=0. Also, μk is the centroid of xi’s cluster.

It’s a minimization problem of two parts. We first minimize J w.r.t. wik and treat μk fixed. Then we minimize J w.r.t. μk and treat wik fixed. Technically speaking, we differentiate J w.r.t. wik first and update cluster assignments (E-step). Then we differentiate J w.r.t. μk and recompute the centroids after the cluster assignments from previous step (M-step). Therefore, E-step is:

![](https://github.com/kshitij-pro/capacitated_clustering/blob/16a72e9d56305c881009b06fced70eaba25889b2/Screenshot%202021-07-31%20173858.png)

In other words, assign the data point xi to the closest cluster judged by its sum of squared distance from cluster’s centroid.

And M-step is:

![](https://github.com/kshitij-pro/capacitated_clustering/blob/6ca845e450e421373f34b3c2965104aa478cf1f2/Screenshot%202021-07-31%20174032.png)

## Modified K-means for CCP
1. Calculate the number of clusters

   Calculated based on the demand (di) of the citiy i and the capacity of the cluster C as
   
   <a href="https://www.codecogs.com/eqnedit.php?latex=k&space;=&space;\left&space;\lceil&space;(\sum&space;_{i=1}^n&space;d_i)/c\right&space;\rceil" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k&space;=&space;\left&space;\lceil&space;(\sum&space;_{i=1}^n&space;d_i)/c\right&space;\rceil" title="k = \left \lceil (\sum _{i=1}^n d_i)/c\right \rceil" /></a>

2. Select initial centroids

   The initial k centroids are selected by arranging the cities based on the decreasing order of demand. The first k cities are initial centroids.
3.  Assign cities to clusters

    The distance between each city to all k centroids are calculated. Group all the cities i to the closest centroid j. To find appropriate centroid j for city i, calculate a priority value-
    
      <a href="https://www.codecogs.com/eqnedit.php?latex=Priority_{i}&space;=&space;cost_{ij}/d_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Priority_{i}&space;=&space;cost_{ij}/d_i" title="Priority_{i} = cost_{ij}/d_i" /></a>
  
    Higher the priority more tempting it is to keep the city i in cluster j
4.  Centroid Calculation

    The centroid (Xj,Yj) for each cluster is calculated based on the member of the cluster.
    
      <a href="https://www.codecogs.com/eqnedit.php?latex=x_j&space;=&space;\sum&space;_{i=1}^mx_i/m\&space;\&space;y_j&space;=&space;\sum&space;_{i=1}^my_i/m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_j&space;=&space;\sum&space;_{i=1}^mx_i/m\&space;\&space;y_j&space;=&space;\sum&space;_{i=1}^my_i/m" title="x_j = \sum _{i=1}^mx_i/m\ \ y_j = \sum _{i=1}^my_i/m" /></a>
    
## Implementation and Result

![](https://github.com/kshitij-pro/capacitated_clustering/blob/b786020791c7b09c13a0b01e63b3409a776984f1/n32_vrp_instance.png)
