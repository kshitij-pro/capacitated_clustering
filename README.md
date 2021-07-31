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


