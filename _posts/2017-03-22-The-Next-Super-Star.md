---
layout: post
title: “The Next Super Star”
#categories: journal
tags: [STA141B final project]
image:
  feature: nbafans.png
  teaser: nbafans-teaser.png
  credit: Death to Stock Photo
  creditlink: ""
---
<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>


## _Motivation_

Given the large basis of NBA audiences and increasing pursue for super stars, using past year data to analyze who is the next super star seems to be an interesting and meaningful question.


## _Questions_

Are there any statistical patterns in the players performance? Can we use the pattern to predict the potential stars?

What features do the potential stars and super stars share?

## _Methodology_

Using NBA statistic data, we would like to do some exploratory analysis and data visualization over “all stars” and “potential players” based on their first four seasons data

1. Data Scrapping

2. K-means Cluster

3. PCA and Data Visualization

4. Compare player A and player B


## _Explanation for Choosing the Methodology_

### Data Scrapping
We exploit the data from http://www.basketball-reference.com/ and used lxml module to extract basic statistics data of rookie players of 2013 during recent four seasons and all starts during recent four seasons.

### k-means

We are interested whether there is any statistical patterns in the statistics of the players' performances. To answer this question, we would like to cluster the data and see if the stars and rookie players can be in the same cluster. Basically, we will mainly use clustering to automatically split players into several clusters based on technical data during the seasons. To deal with the data containing 180 variables, we normalized the data.

Explicitly, we use K-means cluster to group similar players based on the first four year players stats. The main idea is that if a fourth year player share the same cluster as star players, then we can conclude they are similar in terms of early career stats and therefore that young player has the potential to become a star player. However, the number of clusters K need to be pre-specified. Thus, it necessary to evaluate the choice of K. There are many metrics and here we use silhouette scores. The silhouette score for each sample is defined as $s(i)=\dfrac{b(i)−a(i)}{\max{ ( a(i),b(i) ) }}$ where $a(i)$ is the mean distance between a sample and all other points in the same cluster and $b(i)$ is the mean distance between a sample and all other points in the next nearest cluster. So it is clear that $−1 \leq s(i) \leq 1$ where a high value indicates that the object is well matched to its own cluster and poorly matched to neighboring clusters. If most objects have a high value, then the clustering configuration is appropriate. Finally, the Silhouette Coefficient for whole dataset is given as the mean of the silhouette Coefficient for each sample. For the sake of visualization, K-means clustering is run on the dataset for a range of values of k from 2 to 10, and for each value of k the silhouette is calculated. The plot of silhouette scores against different k is shown as follows.

<img src="https://mengxinji.github.io/STA141B/images/slh.png" alt="" width="60%">


We can see the optimal K is 2. This actually makes sense as the data is comprised of both stats for star players (have been proved later on) and 4th-year rookies. Nevertheless, we want to go deeper in order to find more patterns among similar players. For example, star players can also belong to different groups as they may play in different positions therefore their stats are different. Surprisingly, there is a bump when k = 5 and it turns out to be a reasonable choice of k in terms of interpretation and visualization.

## K-means Cluster Results

Cluster 4 is the largest proportion and cluster 1 is the smallest. The players in cluster 2 are mostly rookie players and all the players in cluster 3 are stars. In cluster 1,4, and 3, there are a few players are rookie players. Such that rookie stars in cluster 1, 4, and 3 may be potential candidates for next stars.



<img src="https://mengxinji.github.io/STA141B/images/pieCL.png" alt="" width="30%"> <img src="https://mengxinji.github.io/STA141B/images/stackCl.png" alt="" width="30%">


## PCA Visualization

We use PCA simply because we want to visualize the results on a 2-D plane. We find first two components account for over 60% variance, which turned out to display the cluster groups surprisingly well. However, it is not easy to interpret each PC components as they are relevant to many features. But one key observation is that PC1 is very related to the stats categories regarding 3-pointer shooting.

![alt tag](https://mengxinji.github.io/STA141B/images/cluster_plot_r.png)

As we can see, the cluster 1 is on the top left corner of the plot, which purely consists of super stars. The cluster 4 which on the right of the plot is basically composed of nobodies. Therefore, we are interested in cluster 2, 3 and 5 which are mix of super stars and rookie players. Let’s go through them one by one.

Cluster 5 is very informative since all of the players in cluster 5 are super stars except Victor Oladipo and Michael Carter-Williams. Therefore we can initially conclude those two players have the potential to become super stars. Notice that the difference of cluster 5 than cluster 1 is that it only has guards whereas cluster 1 also has front court players.

Cluster 3 also has some potential super stars such as C.J.McCollum. If we dive into this cluster we can find one key connection between super stars and potential rookies. Note that Paul George, Jimmy Butler and C.J.McCollum were all winners of Most Improved Player Award, which reveals an important information about this group. Many of the player in this group may not play well in their early career, but they improved significantly later on and ended up to be super stars. This is also true for players such as Dirk Nowitzki, Kawhi Leonard and Kyle Lowry. Thus we can further conclude that McCollum, Schroder and Caldwell-Williams are likely to become super stars in the future.

Finally for the cluster 2. Note that this group mainly consists of front court player where we can see several potential big guys such as Giannis Antetokounmpo and Nerlens Noel. Whence we have further evidence that those players have the potential to become future stars that dominate the paint.


## Data Analysis

Based on the results of clustering, we would like to analyze why player A and player B are in the same cluster.
James Harden vs. Micheal Cart-Williams Paul Millsap vs. Nerlen Noel
Tony Parker vs. Victor Oladipo.

For James Harden vs. Micheal Cart-Williams, We compared their 3 point rate during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/James_Michael.png)

For Paul Millsap vs. Nerlen Noel, we compared their BLK during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/Millsap_Noel.png)

For Tony Parker vs. Victor Oladipo, we compared their Field Goal% during last four regular seasons.

![alt tag](https://mengxinji.github.io/STA141B/images/Parker_Oladipo.png)


## Conclusion

Ideally, we would exploit an automatic clustering method that can correctly split all players into several clusters, and based on the similar pattern between all stars and potential stars to identify a forthcoming super star!

Besides the plots we showed above, we test several stats of these 3 pairs, most of the stats have similar distribution, suggesting the rookie players play highly resemble with the star players.

Finally, we can say that this three players Micheal Cart-Williams, Nerlen Noel, Victor Oladipo might become star players in the future.
