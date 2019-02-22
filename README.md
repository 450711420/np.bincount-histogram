# np.bincount-histogram
how to generate histograms of the labels within a second fixed-sized MxM
window that moves over the image (e.g. 25x25) (use np.bincount). Cluster the histograms
using k-means, where K is the number of distinct textures observed in the source image.
