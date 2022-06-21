`Week 3` Exploratory Data Analysis
================

-   👨🏻‍💻 Author: Anderson H Uyekita
-   📚 Specialization: <a
    href="https://www.coursera.org/specializations/data-science-foundations-r"
    target="_blank" rel="noopener">Data Science: Foundations using R
    Specialization</a>
-   📖 Course:
    <a href="https://www.coursera.org/learn/exploratory-data-analysis"
    target="_blank" rel="noopener">Exploratory Data Analysis</a>
    -   🧑‍🏫 Instructor: Roger D Peng
-   📆 Week 3
    -   🚦 Start: Wednesday, 08 June 2022
    -   🏁 Finish: Wednesday, 15 June 2022

------------------------------------------------------------------------

#### Assignments & Deliverables

-   💻 Swirl
    -   Hierarchical Clustering
    -   K Means Clustering
    -   Dimension Reduction
    -   Clustering Example
-   This week there is no 📝 Quiz

------------------------------------------------------------------------

#### Slides

-   Lesson 1: Hierarchical Clustering <a href="" id="lesson-1"></a>
    -   [Hierarchical
        Clustering](./slides/3_1_hierarchical-clustering.pdf)
-   Lesson 2: K-Means Clustering & Dimension Reduction
    <a href="" id="lesson-2"></a>
    -   [K-Means Clustering](./slides/3_2_1_k-means-clustering.pdf)
    -   [Dimension
        Reduction](./slides/3_2_2_principal-components-analysis-and-singular-value-decomposition.pdf)
-   Lesson 3: Working with Color <a href="" id="lesson-3"></a>
    -   [Working with Color](./slides/3-3_colors.pdf)

------------------------------------------------------------------------

#### Description

> Welcome to Week 3 of Exploratory Data Analysis. This week covers some
> of the workhorse statistical methods for exploratory analysis. These
> methods include clustering and dimension reduction techniques that
> allow you to make graphical displays of very high dimensional data
> (many many variables). We also cover novel ways to specify colors in R
> so that you can use color as an important and useful dimension when
> making data graphics. All of this material is covered in chapters 9-12
> of my book Exploratory Data Analysis with R.

------------------------------------------------------------------------

## Class Notes

### [<kbd>Lesson 1</kbd>](#lesson-1) Hierarchical Clustering

Clustering organizes things that are **close** into groups

> -   How do we define close?
> -   How do we group things?
> -   How do we visualize the grouping?
> -   How do we interpret the grouping?

**Hierarchical Clustering**

It is a way to agglomerate data by using a distance method. The result
of it would be a tree.

> -   An agglomerative approach
>     -   Find closest two things
>     -   Put them together
>     -   Find next closest
> -   Requires
>     -   A defined distance
>     -   A merging approach
> -   Produces
>     -   A tree showing how close things are to each other

``` r
library(datasets)
library(magrittr)
library(ggplot2)

# Calculating the distance between mpg and wt variables.
distance_df <- stats::dist(x = data.frame(mpg = mtcars$mpg, wt = mtcars$wt),
                           method = "euclidean")

# Creating the Hierarchical cluster (it is like a tree).
tree <- stats::hclust(d = distance_df)

# Plotting the tree using the base graphic package.
base::plot(x = tree)

# Adding a rectangle to show a hypothesis of 3 clusters.
stats::rect.hclust(tree, 3)
```

![](README_files/figure-gfm/unnamed-chunk-1-1.png)<!-- --> According to
the height, you can decide to cut the tree to produce how many clusters
you want. In this example, I have cut the tree to create 3 groups. So
Let’s use the Hierarchical Clustering output to color a scatter plot.

``` r
# Creating a Data frame with mpg, wt and cluster.
df_cluster <- data.frame(mpg = mtcars$mpg,
                         wt = mtcars$wt,
                         cluster = factor(stats::cutree(tree, 3)))

# Plotting the scatter plot with the cluster as color.
p1 <- df_cluster %>%
    ggplot2::ggplot(aes(x = wt, y = mpg)) + 
    geom_point(aes(color = cluster)) +
    ggtitle("Hierarchical Clustering")

p1
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

**Notes**

-   Gives an idea of the relationships between variables/observations
-   The picture may be unstable
    -   Change a few points
    -   Have different missing values
    -   Pick a different distance
    -   Change the merging strategy
    -   Change the scale of points for one variable
-   But it is deterministic
-   Choosing where to cut isn’t always obvious
-   Should be primarily used for exploration

### [<kbd>Lesson 2</kbd>](#lesson-2) K-Means Clustering & Dimension Reduction

**K-Means Clustering**

The K-means differs from the Hierarchical clustering because you need to
know the number of clusters you want before running the process.

-   A partioning approach
    -   Fix a number of clusters
    -   Get “centroids” of each cluster
    -   Assign things to closest centroid
    -   Reclaculate centroids
-   Requires
    -   A defined distance metric
    -   A number of clusters
    -   An initial guess as to cluster centroids
-   Produces
    -   Final estimate of cluster centroids
    -   An assignment of each point to clusters

``` r
kmeans_results <- kmeans(x = data.frame(mpg = mtcars$mpg, wt = mtcars$wt),
                         centers = 3)

# Creating a Data frame with mpg, wt and cluster.
df_cluster <- data.frame(mpg = mtcars$mpg,
                         wt = mtcars$wt,
                         cluster = factor(kmeans_results$cluster))

# Plotting the scatter plot with the cluster as color.
p2 <- df_cluster %>%
    ggplot2::ggplot(aes(x = wt, y = mpg)) + 
    geom_point(aes(color = cluster)) +
    ggtitle("K-Means Clustering")

p2
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

Comparing Hierarchical and K-means Clustering:

``` r
library(cowplot)
cowplot::plot_grid(p1, p2)
```

![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

**Notes**

-   K-means requires a number of clusters
    -   Pick by eye/intuition
    -   Pick by cross validation/information theory, etc.
-   K-means is not deterministic
    -   Different \# of clusters
    -   Different number of iterations

**Dimension Reduction**

-   Find a new set of multivariate variables that are uncorrelated and
    explain as much variance as possible.
-   If you put all the variables together in one matrix, find the best
    matrix created with fewer variables (lower rank) that explains the
    original data.

**Notes**

-   The first goal is **statistical** and the second goal is **data
    compression**.
-   Scale matters
-   PC’s/SV’s may mix real patterns
-   Can be computationally intensive

### [<kbd>Lesson 3</kbd>](#lesson-3) Working with Color

**Working with Color**

> -   The grDevices package has two functions
>     -   `colorRamp`: Take a palette of colors and return a function
>         that takes valeus between 0 and 1, indicating the extremes of
>         the color palette (e.g. see the ‘gray’ function)
>     -   `colorRampPalette`: Take a palette of colors and return a
>         function that takes integer arguments and returns a vector of
>         colors interpolating the palette (like heat.colors or
>         topo.colors)
> -   These functions take palettes of colors and help to interpolate
>     between the colors
> -   The function colors() lists the names of colors you can use in any
>     plotting function

``` r
library(RColorBrewer)

cols <- brewer.pal(3, "BuGn")
pal <- colorRampPalette(cols)
image(volcano, col = pal(20))
```

![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

> -   The `rgb` function can be used to produce any color via red,
>     green, blue proportions
> -   Color transparency can be added via the alpha parameter to `rgb`
> -   The `colorspace` package can be used for a different control over
>     colors

**Summary**

> -   Careful use of colors in plots/maps/etc. can make it easier for
>     the reader to get what you’re trying to say (why make it harder?)
> -   The RColorBrewer package is an R package that provides color
>     palettes for sequential, categorical, and diverging data
> -   The `colorRamp` and `colorRampPalette` functions can be used in
>     conjunction with color palettes to connect data to colors
> -   Transparency can sometimes be used to clarify plots with many
>     points
