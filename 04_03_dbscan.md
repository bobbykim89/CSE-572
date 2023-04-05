# Density based clustering

DBSCAN algo popular.
Density based.
We consider the entire feature space --> we consider the area
To quantify density you need:

- We get the distance metric (euclidean for example)
- We set a threshold (Eps//radius is threshold)

Geometrically if euclidean is just a circle.
Density == points inside a circle.
If we keep the area consistent, then we can normalize the value of density.

## types of points in DBscan

- core points: points in the interior of the cluster.
  - First define a neighborhood (given particular point, get dist metric like euclidean, manhatan, etc, and a threshold Eps)
  - Threshold: min points... if the number of points close to the center is a min value.
  - You INCLUDE the core point in the count.
- border points: less than min points. Like literally the border point is inside the circle surrounding the core.
  - not a core point
  - in the neighborhood
- noise points: Below minPts and not even on border of A.
  - not a core point
  - not in the neighborhood

## DBscan algorithm

1. Label all points core/border/noise (go thru all data once)
2. Eliminate noise points.
3. We put edge on all core points within EPs of each other. make one big boundary.
4. You will have groups of core points. In one group all ocre points will be connected, you will get islands. Inside EAch island is completely connected.
5. We take each island and name them a separate cluster.
6. We assign each border point to one of the clusters it is in neighborhood of.

### complexity of algorithm

- Time complexity is O(number of points \* time to find points in Eps neighborhood)
  - Labelling all points takes the most time.
- In the worst case then, complexity is O(m^2)
- Worst case is order m for everything else... removing noise, putting edge, connect core pointersm, assign borders.
- Some low dimensional spaces make it O(m log n) but he did not discuss it.
- The space requirement is O(m) you just need cluster label and classification per point.

## thresholds

- We need to figure out EPs and MinPts because they define threshold.
- How to select them... will affect clustering.
- EPS:
  - Depends on what type of clusters you want
  - Depends on geometrical representation
  - Globular clusters... choose euclidean
  - Non-Globular... use L2, L3, L4 norm
- MinPoints:
  - Depends on the inter cluster distance.
  - Too small will make too many clusters... each point a cluster.
  - Too big will make too few... or even just one big cluster.

You can change EPs and plot the no of cluters where NoClusters = f(EPs size) and see where it just goes off the charts (inflection point)

## benefits

- resistant to noise
- can handle clusters of different shapes and sizes

## weaknesses

- issues with varying density clusters
- problems with high dimensional data... density calc takes time
- cna be expensive because we need to calculate neighborhood points

# Knowledge check

1. What type of clustering is DBSCAN

   - Density-based

2. which are true about DBSCAN

   - It has trouble wihen the clusters have widely varying densities
   - DBSCAN has issue with high dimensional data
   - It can be expensive when the computation of nearest neighbords requires computing all pairwise proximities

3. What happens when you increase the value of EPs while keeping MinPoints same?

- Core points may increase
- Border points may reduce

4. What happens when you increase MinPts while keeping EPs same?

- Core points may decrease (you need more points in same neighborhood)
- Core points may become noise points
- Border points may become noise points
