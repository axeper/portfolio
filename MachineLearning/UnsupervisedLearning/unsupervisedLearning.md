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






# Hierarchical Clustering

	Find closest two things -> put them together -> find next closest
	Requires : defined distance, merging approach
	Produces: a tree showing how close things are
	
	Distance metric (pick one that makes sense):
		Continuous - euclidean distance (sqrt(sum(distance)^2))
		Continuous - correlation similarity
		Binary - manhattan distance (sum of absolute distance)

	Example:
	set.seed(1234); par(mar=c(0,0,0,0))
	x <- rnorm(12,mean=rep(1:3,each=4),sd=0.2)
	y <- rnorm(12,mean=rep(c(1,2,1),each=4),sd=0.2)
	plot(x,y,col="blue",pch=19,cex=2)
	text(x+0.05,y+0.05,labels=as.character(1:12))

	dataFrame <- data.frame(x=x,y=y)
	distxy <- dist(dataFrame)
	hClustering <- hclust(distxy)
	plot(hClustering)
	plot(as.dendrogram(hClustering))
	
	# Prettier
	myplclust(hClustering,lab=rep(1:3,each=4),lab.col=rep(1:3,each=4))
	# Even prettier
	http://gallery.r-enthusiasts.com/RGraphGallery.php?graph=79
	
	# Heatmap
	dataMatrix <- as.matrix(dataFrame)[sample(1:12),]
	heatmap(dataMatrix, cm.colors(25))
	
	
# K-means

	Create clusters -> compute centroid -> assign things to closest centroid -> recalculate centroids

	# Example
	dataFrame <- data.frame(x,y)
	kmeansObj <- kmeans(dataFrame,centers=3)
	names(kmeansObj); kmeansObj$cluster;
	
	par(mar=rep(0.2,4))
	plot(x,y,col=kmeansObj$cluster,pch=19,cex=2)
	points(kmeansObj$centers,col=1:3,pch=3,cex=3,lwd=3)

	# one liner
	plot(x,y,col=kmeans(dataFrame,6)$cluster,pch=19,cex=2)


# Dimension reduction

	Let's use a weighted combination to reduce noise and the number of predictors.
	Similarly:
		1) Find a new set of multivariate variables that are uncorrelated and explain as much variance as possible. (statistical goal)
		2) Putting all the variables together in one matrix, we want to find the best matrix created with fewer variables that explains the original data. (data compression goal)	
		
	Solutions:
		PCA:
		The principal components are equal to the right singular values if you first scale (subtract the mean, divide by the standard deviation) the variables.

		SVD: 
		If X is a matrix with each variable in a column and each observation in a row then the SVD is a "matrix decomposition"
		X = U*D*transpose(V)
		where the columns of U are orthogonal (left singular vectors), the columns of V are orthogonal (right singluar vectors) and D is a diagonal matrix (singular values). As they have lower ranks, it's easier to compute/store/etc...
		
		in R:
		svd1 <- svd(scale(dataMatrixOrdered))
		par(mfrow=c(1,3))
		image(t(dataMatrixOrdered)[,nrow(dataMatrixOrdered):1])
		plot(svd1$u[,1],40:1,,xlab="Row",ylab="First left singular vector",pch=19)
		plot(svd1$v[,1],xlab="Column",ylab="First right singular vector",pch=19)

		par(mfrow=c(1,2))
		plot(svd1$d,xlab="Column",ylab="Singular value",pch=19)
		plot(svd1$d^2/sum(svd1$d^2),xlab="Column",ylab="Prop. of variance explained",pch=19)
	
		# If there are missing values, use imputing
		library(impute)  ## Available from http://bioconductor.org
		dataMatrix2 <- dataMatrixOrdered
		dataMatrix2[sample(1:100,size=40,replace=FALSE)] <- NA
		dataMatrix2 <- impute.knn(dataMatrix2)$data
		svd1 <- svd(scale(dataMatrixOrdered)); svd2 <- svd(scale(dataMatrix2))
		par(mfrow=c(1,2)); plot(svd1$v[,1],pch=19); plot(svd2$v[,1],pch=19)

		# Approximating a face with SVD
		svd1 <- svd(scale(faceData))
		approx1 <- svd1$u[,1] %*% t(svd1$v[,1]) * svd1$d[1]
		approx5 <- svd1$u[,1:5] %*% diag(svd1$d[1:5])%*% t(svd1$v[,1:5]) 
		approx10 <- svd1$u[,1:10] %*% diag(svd1$d[1:10])%*% t(svd1$v[,1:10]) 
		
		par(mfrow=c(1,4))
		image(t(approx1)[,nrow(approx1):1], main = "(a)")
		image(t(approx5)[,nrow(approx5):1], main = "(b)")
		image(t(approx10)[,nrow(approx10):1], main = "(c)")
		image(t(faceData)[,nrow(faceData):1], main = "(d)")  ## Original data
	
		* Alternatives
			* [Factor analysis](http://en.wikipedia.org/wiki/Factor_analysis)
			* [Independent components analysis](http://en.wikipedia.org/wiki/Independent_component_analysis)
			* [Latent semantic analysis](http://en.wikipedia.org/wiki/Latent_semantic_analysis)

			
# Case Studies
	
	# Dendograms for quick and dirty analysis
	dMatrix <- dist(sub1[, 10:12])
	hclustering <- hclust(dMatrix)
	myplcluster(hclustering, lab.col = unclass(sub1$activity))
	
	# SVD
	svd1 = svd(scale(sub1[, -c(562,563)]))
	par(mfrow = c(1,2))
	plot(svd1$u[, 1], col = sub1$activity, pch = 19)
	plot(svd1$u[, 2], col = sub1$activity, pch = 19)
	
	# Clustering on max contribution
	maxContrib <- which.max(svd1$v[, 2])
	dMatrix <- dist(sub1[, c(10:12, maxContrib)])
	hclustering <- hclust(dMatrix)
	myplcluster(hclustering, lab.col = unclass(sub1$activity))
	
	# K-means (warning: random initialization)
	kClust <- kmeans(sub1[, -c(562, 563)], centers = 6, nstart = 1)
	table(kClust, sub1$activity)

	
# Case Study

	## setwd("~/CourseraModules/04_ExploratoryAnalysis/CaseStudy/pm25_data")
	## Has fine particle pollution in the U.S. decreased from 1999 to 2012?

	## Read in data from 1999
	pm0 <- read.table("RD_501_88101_1999-0.txt", comment.char = "#", header = FALSE, sep = "|", na.strings = "")
	# Clearer names
	cnames <- readLines("RD_501_88101_1999-0.txt", 1)
	cnames <- strsplit(cnames, "|", fixed = TRUE)
	names(pm0) <- make.names(cnames[[1]])
	
	## Read in data from 2012
	pm1 <- read.table("RD_501_88101_2012-0.txt", comment.char = "#", header = FALSE, sep = "|", na.strings = "", nrow = 1304290)
	names(pm1) <- make.names(cnames[[1]])

	## Five number summaries for both periods
	x0 <- pm0$Sample.Value; x1 <- pm1$Sample.Value
	summary(x1)
	summary(x0)
	mean(is.na(x1))  ## Are missing values important here?

	## Are missing values important here? It depends
	mean(is.na(x1)); mean(is.na(x0)) 
	
	## Make a boxplot of both 1999 and 2012
	boxplot(x0, x1)
	boxplot(log10(x0), log10(x1))

	## Notice if there are unusual (very high, negative) 
	
	## Find a monitor for New York State that exists in both datasets
	site0 <- unique(subset(pm0, State.Code == 36, c(County.Code, Site.ID)))
	site1 <- unique(subset(pm1, State.Code == 36, c(County.Code, Site.ID)))
	site0 <- paste(site0[,1], site0[,2], sep = ".")
	site1 <- paste(site1[,1], site1[,2], sep = ".")
	both <- intersect(site0, site1)

	## Find how many observations available at each monitor
	pm0$county.site <- with(pm0, paste(County.Code, Site.ID, sep = "."))
	pm1$county.site <- with(pm1, paste(County.Code, Site.ID, sep = "."))
	cnt0 <- subset(pm0, State.Code == 36 & county.site %in% both)
	cnt1 <- subset(pm1, State.Code == 36 & county.site %in% both)
	sapply(split(cnt0, cnt0$county.site), nrow)
	sapply(split(cnt1, cnt1$county.site), nrow)

	## Choose in NYC 36, county 63 and side ID 2008
	pm1sub <- subset(pm1, State.Code == 36 & County.Code == 63 & Site.ID == 2008)
	pm0sub <- subset(pm0, State.Code == 36 & County.Code == 63 & Site.ID == 2008)

	## Plot data for 2012
	x1sub <- pm1sub$Sample.Value
	dates1 <- pm1sub$Date
	dates1 <- as.Date(as.character(dates1), "%Y%m%d")
	
	## Plot data for 1999
	x0sub <- pm0sub$Sample.Value
	dates0 <- pm0sub$Date
	dates0 <- as.Date(as.character(dates0), "%Y%m%d")

	## Find global range and make the plots
	rng <- range(x0sub, x1sub, na.rm = T)
	par(mfrow = c(1, 2), mar = c(4, 4, 2, 1))
	plot(dates0, x0sub, pch = 20, ylim = rng)
	abline(h = median(x0sub, na.rm = T))
	plot(dates1, x1sub, pch = 20, ylim = rng)
	abline(h = median(x1sub, na.rm = T))

	## Show state-wide means and make a plot showing trend
	mn0 <- with(pm0, tapply(Sample.Value, State.Code, mean
	mn1 <- with(pm1, tapply(Sample.Value, State.Code, mean, na.rm = T))

	## Make separate data frames for states / years
	d0 <- data.frame(state = names(mn0), mean = mn0)
	d1 <- data.frame(state = names(mn1), mean = mn1)
	mrg <- merge(d0, d1, by = "state")

	## Connect lines
	par(mfrow = c(1, 1))
	with(mrg, plot(rep(1, 52), mrg[, 2], xlim = c(.5, 2.5)))
	with(mrg, points(rep(2, 52), mrg[, 3]))
	segments(rep(1, 52), mrg[, 2], rep(2, 52), mrg[, 3])


	
	
	
	
	
	