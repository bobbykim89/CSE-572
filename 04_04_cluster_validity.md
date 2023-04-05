# Introduction to cluster validity

We need to find out how good is a cluster.
For supervised classification we have the ground truth, but for clustering we dont have it because it is unsupervised.
This is why it is difficult, we dont know the truth.

## reasons why we need analysis/validation of goodness of clusters

- To avoid clustering noise.
- To select the better clustering algorithm.
- to compare two sets of clusters. Each given by a different algo
- For a given algo, compare two clusters.

## example

We compare the following:

- DBSCAN
- K-means
- complete link

## depending factors

- determining clutering tendency of set of data (does it keep evident data characteristics?)
- determining the correct number of clusters (who knows how many are correct?) Based on educated guesses really based on prior info
- Evaluating how well clusters fit data without reference to external info (if we dont have class labels, does it actually fit the data, semantics exist?)
- Comparing clusters results to externally known results. (If we know class labels, we can see if the clustering is matching the labels and see if it keeps data properties.)
- Comparing the results of two different datasets to determine which is better (if you have ext class labels then you can check which one did better)

## Measures of cluster validity

- Unsupervised: we dont have any prior knowledge//external info (sum of square errors)
- Supervised: we have ext data, ie class labels
- Relative: compares different clustering techniques

### Supervised validity

So this one is easier because you have some external data, like class labels
Procedure:

- measure degree of correspondence between cluster labels and class labels (do they match?)
- Compares clustering results vs ground truth
- You do this to compare different clustering approaches because you dont really need clustering if you already have the ground truth.

Once you know which ones is good then you can use the good clustering approach for unsupervised clustering of similar data.

#### measurements supervised

- Entropy: degree of objects belonging to single class.
- Low values: good clusters (high purity)
- High values: bad clusters (low purity)

### Unsupervised validity

we dont have any external information. You can use SSE to measure intra cluster distance.
-SSE

- Plotting SSE vs no of clusters... SSE decreases as # of clusters increase
- SSE only gets intra cluster distance
- SSE does not get inter cluster distance
- SSE will stop at 0 when each point is a cluster

#### metrics

- cluster cohesion WSS: measures the intra cluster distance (how close things are in a cluster)

```math
WSS = \sum\sum({x-m_i}^{2})
```

You get the dist between point and center point... summ them per cluster, and sum all clusters.
You want to minimize WSS for good inter cluster cohesion.

- cluster separation BSS: measures the inter cluster distance (how well separated are clusters)

```math
BSS = \sum|C_i|({m-m_i}^{2})
```

You find distances between center of each cluster and the overall mean of the data. Then we weigh the distance wrt total no of items in each cluster... then sum it up.
You want to maximize BSS for good intra cluster separation.

#### relation between cohesion and separation

If you minimize WSS == maximization BSS
They are two sides of the same coin. They are connected.

- WSS + BSS = constant.... the total sum of squares TSS
- TSS: the distance of each point ot the overall mean of the data.

#### silhouette coefficient

1. calculate avg distance for point i to all other objs in its cluster. You call that a.
2. We look at all other clusters, we take this point i and calculate dists for objs in all other clusters. You get the min distance and call that b.
3. You calculate the silhouette as:

```math
S_i = \frac{b_i-a_i}{max(a_i,b_i)}
```

bi is the min inter cluster distance.(in knowledge check this was mean)
ai is the average intra cluster distance.

If an algo maximizes inter and minimizes intra, then you have a high silhouette coefficient.

Best case scenario Si ~ 1

You can give each point a silhouette coefficient. A middle point in between clusters will have a low Si.

#### correlation

- You create a matrix with one row and one column for each data point. For points that belong to a cluster, you give them the same similarity value==1.
- If pair belongs to different clusters, then you assume no similarities at all so value==0.
- You end up with an ideal similarity matrix. In reality no points are exactly same.
- you basically check the actual similarity matrix and check how close it is how close it is to the ideal similarity matrix.
- If correlation is high (matrices are similar to each other), then clustering is close to ideal and it is good.
- You want to get corr == 1 as best

You can literally plot the similarity matrix... where high colors means they belong to same cluster. The matrix should have like very clear and sharp images.

## Knowledge check

1. What is the purpose of cluster analysis?
   - To avoid finding patterns in noise
   - To compare clustering algorithms
   - To compare two sets of clusters
     - We do cluster validity to avoid clustering noise and find a suitable algorithm for our data.
2. Select the different aspects of cluster validation.
   - Comparing the results of a cluster analysis to externally known results
     - Cluster validation helps measure the extent to which a clustering structure matches some external structure or in some cases class labels.
   - Determining the ‘correct’ number of clusters
     - Using cluster validation, we can find clustering with optimal cohesion and separation.
   - Compare and decide between the set of clusters on a dataset
     - Cluster validation allows for checking quality of clusters.
3. What is the difference between supervised cluster validity and supervised classification?
   - In supervised cluster validation, class labels are used only after clustering is done, but in supervised classification, class labels are used during the training phase to tune the model.
     - In clustering class labels are used after the clustering process to validate the clustering results.\

Consider the following dataset for 7 subjects with two attributes (A and B) per subject.

| **Subject** | **A** | **B** |
| ----------- | ----- | ----- |
| 1           | 1.0   | 1.0   |
| 2           | 1.5   | 2.0   |
| 3           | 3.0   | 4.0   |
| 4           | 5.0   | 7.0   |
| 5           | 3.5   | 5.0   |
| 6           | 4.5   | 5.0   |
| 7           | 3.5   | 4.5   |

4. K-Means clustering is used with K = 2 clusters and initial centroids are the subjects 1 and 4. Using Euclidean distance, compute the final clusters.
   - Cluster 1:{1,2}, Cluster 2:{3,4,5,6,7}
5. A novel clustering algorithm called AsuCluster suggests the following two clusters: {3,4,5,6,7} and {1,2}. To validate the clusters, compute the SSE for this clustering.
   - 8.53
6. A novel clustering algorithm called AsuCluster suggests the following two clusters: {3,4,5,6,7} and {1,2}. To validate the clusters, compute the sum of Silhouette coefficient for all samples of this clustering.
   - 4.515
