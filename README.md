# Glass Classification using unsupervised learning

## Density Graph Visualization

The density graphs for each feature and the correlation matrix are generated. Mg feature density graph as an example
is shown below. Interpreting the correlation matrix with the help of the density graphs, we can have the following
conclusions and evidence supporting such conclusions. First of all, the 0.81 correlation
coefficient at the first column implies that RI has a fairly strong positive relationship with Ca.
This is why the density graphs of Ca and RI have the similar tendency. Then the values from the
second and the third column implies that Na, Mg, and Al have weak relationships with others.
The -0.55 correlation coefficient at the fifth column implies that Si has a moderate negative
relationship with RI. Therefore, the correlation matrix can tell us the relationship between each
feature.

![Mg feature density graph](https://github.com/ZhengqiY/unsupervised_learning/blob/master/DensityGraphMg.PNG)
![Confusion Matrix](https://github.com/ZhengqiY/unsupervised_learning/blob/master/ConfusionMatrixGlassClassification.PNG)

## Preprocess

Since there are 9 features, the largest number of components that we can choose is 9. In
order to reduce the dimensionality of the data, we set the number of components at 2. According
to the evaluation section, PCA does not help the performance of the following algorithms and
this dataset.

## Clustering

- K-Means
This algorithm updates the centroids until the centroids do not change significantly. We
take k samples and cluster them to the closest centroid. From the results of this step, we update
the centroids by taking the mean value of the k samples. Then algorithm repeats such process
until it meets a threshold. In order to solve the local optimal reached but not global optimal issue,
we applied the k-means++ algorithm, which effectively initializes the centroids.

- Mean-shift
This algorithm updates the centroids by eliminating near-duplicates. The centroid
candidates are updated through a mean shift vector that is computed for each centroid that points
towards a region of the maximum increase in the density of points. This algorithm is guaranteed
to converge but it will stop when the change is not significant.

- Affinity Propagation
This algorithm updates the responses between pairs of samples until convergence. The
responses between pairs represent the suitability. This algorithm is appropriate for small to
medium sized datasets.

## Evaluation

The criteria used were adjusted rand score, completeness score, homogeneity
score, and v measure score. The adjusted rand score computes a similarity measure between two
clusters by considering all pairs of samples and counting pairs that are assigned in the same or
different clusters in the predicted and true clusters. It also ensures to have a value close to 0 for
random labeling independently of the number of clusters and samples and exactly 1 when the
clusters are identical. Completeness score measures if all the data points that are members of a
give class are elements of the same cluster. The homogeneity score measures if all of its clusters
contain only data points which are members of a single class. The v measure score is the
harmonic mean between homogeneity and completeness.

Overall, we noticed that with the PCA reduction the performance of algorithm does not
necessarily improve.
- K-means: Without PCA reduction, we obtained 0.48 completeness score, 0.40
homogeneity score, 0.43 v measure score, and 0.27 adjusted rand score. With PCA reduction, we
obtained 0.47 completeness score, 0.37 homogeneity score, 0.38 v measure score, and 0.24
adjusted rand score.
- Mean-shift: Without PCA reduction, we obtained 0.54 completeness score, 0.41
homogeneity score, 0.47 v measure score, and 0.27 adjusted rand score. With PCA reduction, we
obtained 0.48 completeness score, 0.36 homogeneity score, 0.42 v measure score, and 0.25
adjusted rand score.
- Affinity Propagation: Without PCA reduction, we obtained 0.34 completeness score, 0.54
homogeneity score, 0.42 v measure score, and 0.19 adjusted rand score. With PCA reduction, we
obtained 0.33 completeness score, 0.50 homogeneity score, 0.40 v measure score, and 0.18
adjusted rand score.
Therefore, the mean-shift is the better algorithm to be applied on this dataset not only the
regular case but also the PCA-reduced case.

