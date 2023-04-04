# Introduction to clustering

Clustering is finding groups of objects so that they are similar to one another and different from the objects in other groups.

The only characteristic we explore are attributes in the data.

Definition of cluster depends on whos seen the data. we do not know the ground truth.

It is unsupervised learning problem. Because of that it is difficult to figure out the cluster. Different people will have different definitions. Definition is ambiguous.

A possible distance metric... intra cluster distances are very small + inter-cluster distances are maximized.

Cluster is very dependent on the application.

Many different types of cluster:

- hierarchical -- Set of nested clusters organized as a hierarchical tree. These may interset. In fact one subset can eat another subset. Root node is the cluster containing all the objects.
  - Sometimes it is represented as a dendrogram (think dendrites) to explain the hierarchy
- partitional -- divide onto non overlapping subsets. One object does not belong to more than one subset.

Others...

- exclusive vs non exclusive : non-exclusive a point may belong to different cluster (person can be student and employee at a uni)
- Fuzzy vs non fuzzy: points are weighted, so all the weights sum to 1. fuzzy can be converted to non-fuzzy by enforcing a threshold on the weights.
- Partial vs complete: Noise/outliers are ignored. We dont want to cluster them.
- Heterogeneous vs homogeneous clustering: clustering of wildly different shapes sizes.

## Types of clusters

- Well separated clusters
  - Any point in the cluster is closer to point in cluster as opposed to any non cluter point. IDEALISTIC definition. Inter vs Intra distances essentially.
- center-based
  - An object is closer to the center of the cluster than other cluster centers. You need to calculate the center of the cluster (centroid or medoid).
- contiguous
  - Nearest neighbor notion. closer to one or more points in cluster. You need a distance metric, and you have to be within a specific threshold of distance. Point belongs to cluster if distance to previous points in cluster below some threshold. Think BLOBS.
  - If you want a single cluster then this one does not work.
- density-based
  - Figure out definition of density. ex no of points per sqft. If that is greater than threshold, then they are part of cluster.
  - Gets rid of problems from contiguous.
- property or conceptual
- described by objective function
  - Find clusters that minimize or maximise an objective function.
  - It is a more general approach, kinda a generic definition of all previous ones.

# K Means algorithm

Pretty simple algorithm. Partitional clustering so each cluster is separate from each other, and each has a centroid.

You find the centroid and find out which centroid your point is closest to.
You need to define your number of clusters K.

1. Select K clusters centroids (semi random)
2. For training point i find closest centroid
3. Update the centroid
4. Rinse and repeat until centroids dont change

Closeness: euclidean, correlation, cosine similarity, etc.
Converges in a few iterations.

Weird behavior though. It is kinda dependent on the initial centroids selected. It may find some convergence and does not care that the blobs look odd.

The bottom line, this highly depends upon the initial conditions (centroid guess step 1)

## Bisecting K means

K means has a problem with initial conditions.

Once you get your clusters, you can evaluate your clusters given a sum of squared error.

```math
SSE = \sum \sum {dist}^{2}
```

Distance is the distance of every datapoint relative to the mean of that cluster.

then you sum the errors of each clusters.

Then you can use this SSE to minimize the intra distance and maximizes the inter distance. which is what you want really. IF the number of clusters is fixed.

Some problems:

- selecting initial points (initial centroid problem)
- There should be at least one point in each cluster.
- As number of clusters K grows, then your chances of having an empty cluster grows.
- So the more K points you have, there is a chance the algo gets clusters without a good centroid.

Solutions:

- Multiple runs and select the top 5 top 10 centroids.
  - The hope is that every run will select very different centroids.
  - It may not work 100%, but the probability gets better.
- Run a different clustering algorithm first
  - You use it on step 0 to get initial cluster centroids
  - Better solution and works better
- Select a bunch of K centroids for the same cluster, and then select the centroid that looks the best amongst them
- Bisecting K means
- You can update centroids incrementally
  - We first choose initial clusters. Then we take one datapoint and put it into a cluster.
  - Inmediately after adding a point, you update the centroid of that cluster.
  - Found to improve a lot the K-means.

## Bisecting what it does

1. You take all the datapoints in the cluster and divide into two.
2. Select the cluster that has:
   1. Largest cluster or
   2. Highest SSE cluster or
   3. A combination of both
   4. Densest cluster
   5. Least dense cluster
   6. etc etc
3. You choose the best cluster and divide that cluster into two.
4. rinse and repeat until reaching K no of clusters

The hope is that if no if clusters K is small, then the chances that two points fall in each cluster is much higher.

This is how we solve the issue of initial centroids.

Bisecting splits clusters 2 at a time, discards the ugly one, and once it reaches K it stops.

## why it struggles less

because it does bisections and does not perform multi cluster initial centroid choice. It only chooses 2 centroids.

## SUMMARY K means strengths and weaknesses

### strengths

- very simple and just one pass through the data. Used for wide varieety of data types..
- Efficient even though it may need multiple runs.
- Some variants like bisecting K-means less susceptible to initialization problems.

### weaknesses

- it cannot handle non globular clusters.
- If it is heterogeneous it does not work (like different densities).
- Has trouble clustering data with outliers.

# Knowledge check 1

1. Select the qualities of clusters produced by a good clustering algorithm.

- Intra-cluster distances are minimized.
- Inter-cluster distances are maximized.

2. Select all of the different types of clusters.

- Contiguous
- Density-based
- Center-based
- Well-separated

3. Question 3
   Is it possible that the assignment of samples to clusters does not change between successive iterations in K-Means?

- Yes, When the K-Means algorithm has reached the local or global minima, it will not alter the assignment of samples to clusters for two successive iterations.

4. Clustering is:

- Unsupervised Learning: Correct! You do not have the ground truth for clustering.

5. What is the significance of class label in clustering?

- It is not used in the clustering process... Class label is external information that is not available during the clustering process.

6. What are some of shortcomings of K-means clustering?

- Trouble with non-globular clusters
- Sensitive to outliers and noise
- Trouble with clusters of different sizes and densities.
- Sensitive to initial choice of centers for clusters

7. Consider the following dataset with 7 subjects and two attributes (A and B) per subject.
   ...

Consider that we want to use K-means clustering with K = 2 clusters. Initial centroids are the subjects 1 and 4. Using Euclidean distance, compute the updated centroids after the first iteration in K means.

1 / 1 point

- Centroid 1 : {1,2,3}, Centroid 2: {4,5,6,7}

8. Why does Bisecting K means solve the initial centroid problem?

- Bisecting K means only selects two centroids at a time and hence chance of selecting a wrong centroid is reduced.
