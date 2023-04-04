# Non- partitional clustering

## hierarchical clustering

- agglomerative: You start from each point being a cluster. Then you start merging closest pair of clusters.
- Divisive: start with a single cluster and you divide the data to smaller clusters. You saw an example with bisecting k-means.

## Hierarchical clustering (agglomerative)

Set of nested clusters. Can view it in a dendogram.
Dendogram: tree diagram with the merge/split records.

If we have a specific number of clustering, we can cut the dendogram at a desired position. (so instead of 8 clusters, cut at 4)

We can reduce hierarchical clustering into K means (no of clusters)

### Strengths

- Does not have to assume any particular number of clusters
- They may correspond to meaningful taxonomies. It may actually group the data into classes. (observed in biology data)

### Agglomerative algorithm

1. compute the proximity matrix (define distance, manhattan, euclidean) among all points
2. Let each point be its own cluster.
3. repeat as needed:
   1. Merge the two closest clusters
   2. Update the proximity matrix (among clusters instead of points)
4. Stop when you have 1 cluster only.

Key operation: calculating the distance between two clusters

### computing distance between clusters

- MIN: proximity between closest two points in different clusters
- MAX: proximity between farthest two points in different clusters
- Group Average: gets average of all the distances (pairwise proximity) between points in different clusters
- Centroids: calculate centroids on each cluster and calculate distance between them.
- Other methods driven by objective function (Wards method uses squared error)

These are also used in graph theory.

### Proximity matrix

- if distance matrix:
  - symmetric
  - diagonal is zeros

### example... merging with proximity matrix

When updating proximity matrix:

1. Get the lowest distance in prox matrix
2. Merge the points with lowest distance... consider them as 1 new point
3. Select approach to calculate distances between points...
4. Say Max approach, you get the distance of an unmerged point i and merged points i, j
5. Since youre using max, you get the max distance between these two merged points
6. Update proximity matrix with the max distance of the two
7. Rinse and repeat until you merge everything

### Performance analysis

How distance calculation types perform?

- MIN

  - handles non elliptical shapes
  - handles different cluster sizes
  - very susceptible to noise and outliers (will not really do well)

- MAX

  - not susceptible to outliers
  - Not good with different sizes, will try to break the bigger one.

- Group average
  - tries to get the best of both approaches
  - less susceptible to noise and outliers
  - compromise between single and complete links
  - BIASED towards globular clusters. Will try convex shapes to clusters.

time space requirements:

- O(N2) space because you need to store the proximity matrix
- O(N3) time because there are N steps and for each step the N2 prox matrix needs to be searched/updated
  - complexity can be reduced using advanced data structs like sorted list or heap.
