# Hierarchical Clustering

## hclust

Does hierarchical clustering. Supply a distance matrix.

- Distance: calculate distance between pairs of data points.
	- Euclidean Distance
	- Mahalanobis Distance
	- Minkowski Distance
- Linkage: determines how points are aggregated into clusters.
	- Single linkage: closest minimum distance
	- Complete linkage: closest maximum distance
	- Centroid linkage: lowest centroid distance
	- Ward linkage: lowest error sum of square (ESS) values
	- Average linkage: lowest average distance

hclust uses complete linkage in default.

## cutree

Cut the result into `n` number of trees or according to `h` height

## Intra-cluster distance

Calculated with medoids, centroids, or means of the clusters. Medoids are restricted to be members of the clusters.

## Plot rectangles

First call `plot(hclust(d))`, d being the distance matrix.
Then call `rect.hclust(hclust(d),h=n)`, n being the height threshold.

## Sources

[Distance and linkage](https://levelup.gitconnected.com/distance-measures-and-linkage-methods-in-hierarchical-clustering-8b7d488d7ebc)
