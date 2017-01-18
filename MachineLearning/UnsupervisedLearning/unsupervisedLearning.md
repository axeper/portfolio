### K-means

* Set N clusters
* Choose a distance metric (e.g. euclidian distance) and compute the distance between each clusters
* Optimize the clusters positions to minimize the sum of distances data-clusters
* Compute the [silhouette](https://infogalactic.com/info/Determining_the_number_of_clusters_in_a_data_set#The_Silhouette_Method) to see how N compares 

Minimize within-cluster deviations: k-means + euclidian(float) 

Spherical k-means: k-means + cosine distance

> install.packages("skmeans",dependencies = TRUE)
> library(skmeans)
> winedata <- read.csv("WineKMC.csv")
# Preprocess
> winedata[is.na(winedata)] <- 0
> winedata.transposed <- t(winedata[,8:107])
> winedata.clusters <- skmeans(winedata.transposed, 5, method="genetic")
# Group by clusters
> winedata.clustercounts <-
t(aggregate(winedata.transposed,
by=list(winedata.clusters$cluster),sum)[,2:33])
> winedata.desc.plus.counts <- 
cbind(winedata[,1:7],winedata.clustercounts)
# Show data by the first cluster
> winedata.desc.plus.counts[order(-winedata.desc.plus.counts[,8]),]


### K-medians

Minimize absolute deviations: k-medians + manhattan distance(binary) or cosine distance(asymmetric, i.e. more weight on 1 than 0)


Other k-medioids + other distance






### Hierarchical Clustering