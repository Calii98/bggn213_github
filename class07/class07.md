# Class07: Machine Learning 1
Caliope Marin (PID: A13912583)

Before we get into clustering methods lets make some sample data to
cluster where we know that the answer should be.

To help with this I will use the `rnorm()`function.

``` r
hist(rnorm(150000, mean=-3))
```

![](class07_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
n=10000
hist( c(rnorm(n, mean=3), rnorm(n, mean=-3)))
```

![](class07_files/figure-commonmark/unnamed-chunk-2-1.png)

``` r
n=30
c( rnorm(n, mean=3), rnorm(n, mean=-3) )
```

     [1]  3.611733  2.895279  3.425870  2.509384  4.888254  3.204922  3.005996
     [8]  4.033678  3.043991  2.386782  2.310182  2.370102  2.994243  2.819622
    [15]  2.040334  3.967018  4.781319  2.641570  2.584684  2.988075  2.622295
    [22]  3.992775  1.959663  3.323338  3.571179  3.830430  1.336880  2.210683
    [29]  3.264370  4.238792 -4.115746 -4.647588 -2.347951 -3.106356 -2.172650
    [36] -3.079425 -3.105898 -3.191561 -4.176041 -4.082565 -3.500220 -4.090949
    [43] -2.718196 -2.847604 -2.562917 -3.633655 -4.193834 -2.913512 -3.704885
    [50] -2.766328 -2.581476 -2.362259 -3.563247 -1.798940 -3.296718 -2.824126
    [57] -3.208804 -4.600030 -1.816634 -4.072766

``` r
n=30
x <- c(rnorm(n, mean=3), rnorm(n, mean=-3) )
y <- rev(x)

z <- cbind(x, y) #rbind can combine data fram argument by columns and cbind combines by columns 
z
```

                  x         y
     [1,]  2.862093 -3.994961
     [2,]  2.203686 -3.085244
     [3,]  2.244336 -3.012090
     [4,]  3.918391 -4.463579
     [5,]  1.938038 -2.985315
     [6,]  2.725993 -2.171381
     [7,]  3.469846 -1.934648
     [8,]  3.909296 -3.509875
     [9,]  2.380502 -2.923577
    [10,]  2.182049 -5.004684
    [11,]  2.914335 -2.691505
    [12,]  4.224674 -3.532912
    [13,]  2.507689 -2.758086
    [14,]  3.247107 -3.209519
    [15,]  4.235518 -2.787139
    [16,]  4.106955 -3.251533
    [17,]  2.541402 -2.798436
    [18,]  2.258433 -3.051428
    [19,]  2.751983 -2.986340
    [20,]  3.106077 -2.850660
    [21,]  3.611179 -1.897803
    [22,]  3.664467 -4.261978
    [23,]  2.658498 -2.922650
    [24,]  3.510884 -2.651929
    [25,]  2.953709 -3.996007
    [26,]  4.862335 -3.663897
    [27,]  4.125826 -3.538328
    [28,]  5.025055 -3.528600
    [29,]  3.092734 -2.881400
    [30,]  1.479204 -1.621802
    [31,] -1.621802  1.479204
    [32,] -2.881400  3.092734
    [33,] -3.528600  5.025055
    [34,] -3.538328  4.125826
    [35,] -3.663897  4.862335
    [36,] -3.996007  2.953709
    [37,] -2.651929  3.510884
    [38,] -2.922650  2.658498
    [39,] -4.261978  3.664467
    [40,] -1.897803  3.611179
    [41,] -2.850660  3.106077
    [42,] -2.986340  2.751983
    [43,] -3.051428  2.258433
    [44,] -2.798436  2.541402
    [45,] -3.251533  4.106955
    [46,] -2.787139  4.235518
    [47,] -3.209519  3.247107
    [48,] -2.758086  2.507689
    [49,] -3.532912  4.224674
    [50,] -2.691505  2.914335
    [51,] -5.004684  2.182049
    [52,] -2.923577  2.380502
    [53,] -3.509875  3.909296
    [54,] -1.934648  3.469846
    [55,] -2.171381  2.725993
    [56,] -2.985315  1.938038
    [57,] -4.463579  3.918391
    [58,] -3.012090  2.244336
    [59,] -3.085244  2.203686
    [60,] -3.994961  2.862093

``` r
plot(z)
```

![](class07_files/figure-commonmark/unnamed-chunk-4-1.png)

\##K means clustering

The function in base R for k-means clustering is called `k-means()`.

``` r
km <-kmeans(z, centers=2) # assigns data points to the center data points 
#c;uster size is 30 because n is equal to 30, 
#cluster vector for each point its measuring which cluster is # closer to the center
```

``` r
km$centers
```

              x         y
    1 -3.132244  3.157076
    2  3.157076 -3.132244

Q. Print out the cluster membership vector (i.e our main answer)

``` r
km$cluster
```

     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

``` r
plot(z, col=c("red", "blue")) #if you do this it will repeat each point 
```

![](class07_files/figure-commonmark/unnamed-chunk-8-1.png)

``` r
#you can color it by number 

plot(z, col=2)
```

![](class07_files/figure-commonmark/unnamed-chunk-9-1.png)

Plot with clustering result

``` r
# in order to separate the colors of each cluster
plot(z, col=km$cluster)
points(km$centers, col="blue", pch=15, cex=2) #pch=15 makes a #filled blue square
```

![](class07_files/figure-commonmark/unnamed-chunk-10-1.png)

``` r
#cex stands for character expansion so greater than 1 makes 
#it greater thsn the characters
```

Q. Can you cluster our data in `z` into four clusters please?

``` r
km4 <- kmeans(z, centers = 4)
plot(z, col=km4$cluster)
points(km4$centers, col="blue", pch=15, cex=2)
```

![](class07_files/figure-commonmark/unnamed-chunk-11-1.png)

\##Hierarchical Clustering

The main function for hierarchical clustering in base R is called
`hclust()`

Unlike `kmeans()` I cannot just pass in mt data as input, I first need a
distance matrix from my data.

``` r
d <-dist(z)
hc <-hclust(d)
hc
```


    Call:
    hclust(d = d)

    Cluster method   : complete 
    Distance         : euclidean 
    Number of objects: 60 

There is a specific hclut plot () method…

``` r
plot(hc)
#all the numbers from 1-30 are on onside and the other is #above 30 
abline(h=10, col="red")
```

![](class07_files/figure-commonmark/unnamed-chunk-13-1.png)

To get my main clustering result(i.e. the membership vector) I can “cut”
my tree at a given height. To do this, I will use the `cutreee()`

``` r
grps <- cutree(hc, h=10)
plot(z, col=grps)
```

![](class07_files/figure-commonmark/unnamed-chunk-14-1.png)

\#Principal Component Analysis

Principal component analysis (PCA) is a well established “multivariate
statistical technique” used to reduce the dimensionality of a complex
data set to a more manageable number (typically 2D or 3D). This method
is particularly useful for highlighting strong paterns and relationships
in large datasets (i.e. revealing major similarities and diferences)
that are otherwise hard to visualize.

## PCA of UK food data

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url, row.names=1)
```

Q. 1 How many rows and columns are in your new data frame named x? What
R functions could you use to answer this questions?

``` r
#I can use `nrow()` and `ncol()` to show number of #rows and columns
nrow(x)
```

    [1] 17

``` r
ncol(x)
```

    [1] 4

\##preview the first 6 rows

``` r
head(x)
```

                   England Wales Scotland N.Ireland
    Cheese             105   103      103        66
    Carcass_meat       245   227      242       267
    Other_meat         685   803      750       586
    Fish               147   160      122        93
    Fats_and_oils      193   235      184       209
    Sugars             156   175      147       139

``` r
# Note how the minus indexing works
rownames(x) <- x[,1]
x <- x[,-1]
head(x)
```

        Wales Scotland N.Ireland
    105   103      103        66
    245   227      242       267
    685   803      750       586
    147   160      122        93
    193   235      184       209
    156   175      147       139

``` r
dim(x)
```

    [1] 17  3

``` r
x <- read.csv(url, row.names=1)
head(x)
```

                   England Wales Scotland N.Ireland
    Cheese             105   103      103        66
    Carcass_meat       245   227      242       267
    Other_meat         685   803      750       586
    Fish               147   160      122        93
    Fats_and_oils      193   235      184       209
    Sugars             156   175      147       139

``` r
barplot(as.matrix(x), beside=T, col=rainbow(nrow(x)))
```

![](class07_files/figure-commonmark/unnamed-chunk-21-1.png)

``` r
barplot(as.matrix(x), beside=F, col=rainbow(nrow(x))) #making `beside=F` will
```

![](class07_files/figure-commonmark/unnamed-chunk-22-1.png)

``` r
#make the plot stack all the categories on top of eachother,not pleasant to #look at
```

``` r
pairs(x, col=rainbow(10), pch=16)
```

![](class07_files/figure-commonmark/unnamed-chunk-23-1.png)

\#PCA to the rescue

The main function to do PCA in base R is called `prcomp()`.

Note that I need to take the transpose of this particular data as that
is what the `prcomp()` help page was asking for.

``` r
pca <- prcomp( t(x) ) #t stands for #transpose of x
summary(pca)
```

    Importance of components:
                                PC1      PC2      PC3       PC4
    Standard deviation     324.1502 212.7478 73.87622 2.921e-14
    Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

Whats inside of the object `pca`

``` r
attributes(pca)
```

    $names
    [1] "sdev"     "rotation" "center"   "scale"    "x"       

    $class
    [1] "prcomp"

``` r
#use x to plot main result figure
pca$x
```

                     PC1         PC2        PC3           PC4
    England   -144.99315   -2.532999 105.768945 -9.152022e-15
    Wales     -240.52915 -224.646925 -56.475555  5.560040e-13
    Scotland   -91.86934  286.081786 -44.415495 -6.638419e-13
    N.Ireland  477.39164  -58.901862  -4.877895  1.329771e-13

to make our main result figure, called a “PC plot” (or “score plot”,
“ordination plot” or “PC1 vs PC2 plot”).

``` r
# Plot PC1 vs PC2
plot(pca$x[,1], pca$x[,2],  col= c( "black", "red", "blue", "darkgreen"), pch=16, xlab="PC1 (67.4%)", ylab="PC2 (29%)") 
abline(h=0, col="gray", lty=2)
abline(v=0, col="gray", lty=2)
text(pca$x[,1],pca$x[,2], colnames(x))
```

![](class07_files/figure-commonmark/unnamed-chunk-26-1.png)

``` r
v <- round( pca$sdev^2/sum(pca$sdev^2) * 100 )
v
```

    [1] 67 29  4  0

``` r
## or the second row here...
z <- summary(pca)
z$importance
```

                                 PC1       PC2      PC3          PC4
    Standard deviation     324.15019 212.74780 73.87622 2.921348e-14
    Proportion of Variance   0.67444   0.29052  0.03503 0.000000e+00
    Cumulative Proportion    0.67444   0.96497  1.00000 1.000000e+00

``` r
barplot(v, xlab="Principal Component", ylab="Percent Variation")
```

![](class07_files/figure-commonmark/unnamed-chunk-27-1.png)

``` r
par(mar=c(10, 3, 0.35, 0))
barplot( pca$rotation[,1], las=2 )
```

![](class07_files/figure-commonmark/unnamed-chunk-28-1.png)

\#Variable Loadings Plot

Can give us insight on how the original variables (in this case the
foods contribute to our new PC axis)

``` r
par(mar=c(10, 3, 0.35, 0))
barplot( pca$rotation[,1], las=2 )
```

![](class07_files/figure-commonmark/unnamed-chunk-29-1.png)

``` r
barplot( pca$rotation[,2], las=2)
```

![](class07_files/figure-commonmark/unnamed-chunk-29-2.png)
