Geosci 541 – Paleobiology
Lab Exercise #8 (3/28/16)
Ben Davis Barnes
Problem Set 1

1) Modern-day North America lies to the west of its Cretaceous position.
2) plot() is a function which produces a plot. The first argument identifies the source of data, col= indicates the rgb color setting to be used (red, green, blue vectors, and alpha transparency), lty= indicates the line type to be used (different gradients of solid or dashed patterns), and add=TRUE indicates that the modern map should be added to the existing plot.
3)
> AlbianMap <- downloadPaleogeography(Age=110)
> plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0.01,add=TRUE)

4) Since the Albian, the Eurasian continent has generally moved south, while Africa, India, and Australia have generally moved north-east (particularly the Indian subcontinent and Australia).
