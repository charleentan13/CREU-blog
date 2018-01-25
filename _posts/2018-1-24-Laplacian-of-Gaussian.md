I was having problem to let the algorithm detect peaks consistently without relying on me changing parameters a lot. I was researching online and found some algorithm dealing with edge/blob detection in computer vision. 

I think to some extent; peak detection can be seen as edge/blob detection on one dimension. The peaks in a set of data can be seen as blobs (or a set of two edges) on one dimension. In addition, it seems like blob detection algorithms have been studied extensively by the research community. So I think if I apply the existing methods in blob detection to one dimensional data, it is possible to detect peaks in a reasonably well way without relying on me changing parameters much. 

One such method is the Laplacian of Gaussian method. The original method (which is applied on 2D images) involves first smoothing the image with a Gaussian smoothing filter to reduce effects of noises, and then use convolution to calculate the Laplacians at different pixels (for a detailed description of how the it works on 2D images, see http://ieeexplore.ieee.org/document/4767838/#full-text-section) . The same method can be reduced to 1D case, which corresponds to the peak detection problem I’m solving right now.

In 1D, Laplacian can be calculated as
![plot]({{ site.url }}/assets/1DLaplace.png)
which is the same as taking the second derivative with respect to x. 

In 1D, Gaussian function is defined as
![plot]({{ site.url }}/assets/Gaussian.png)
where sigma and mu are standard deviations and mean respectively. 

Essentially, the algorithm will consist the following steps:
1.	Convolve the data with a 1D Gaussian kernel
2.	Convolve the data with a Laplacian kernel
3.	Find the point where the output value is the highest

There is one issue: how do we select the standard deviation of the Gaussian used in convolution? Based on my understanding, we need to run the algorithm multiple times with different standard deviation values, and then normalize the results, so that we can find the points with highest response across scales. The normalization is explained here: https://math.stackexchange.com/questions/486303/normalized-laplacian-of-gaussian. 

I still need to figure out exactly how to implement the algorithm. 
