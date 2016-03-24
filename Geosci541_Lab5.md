Geosci 541 Ð Paleobiology
Lab Exercise #5 (2/22/16)
Ben Davis Barnes

> Stellar, 20/20, I kind of want to give you extra points.

## Problem Set 1

1) Bivalve generic richness in the Miocene:

````R
> length(BivalveAbundance[which(BivalveAbundance["Miocene",]!=0)])
[1] 634 unique genera in the Miocene
````

2) The Berger-Parker index for Pliocene Brachiopod genera?

````R
> max(BrachiopodAbundance["Pliocene",])/sum(BrachiopodAbundance["Pliocene",])
[1] 0.2222222
````

3) Gini-Simpson Index of Brachs in Late Ordovician?

````R
> LOrdBrachs <- c(BrachiopodAbundance["Late Ordovician",])
> sum(BrachiopodAbundance["Late Ordovician",])
[1] 6154
> 1-sum((LOrdBrachs/6154)^2) 
[1] 0.9784588
````

4) ShannonÕs Entropy of Bivalves in the Late Cretaceous?

````R
> N <- sum(BivalveAbundance["Late Cretaceous",])
> n <- BivalveAbundance["Late Cretaceous",]
> n <- n[which(n!=0)]
> -sum((n/N)*log(n/N))
[1] 5.086654
````

5) ShannonÕs Entropy of Bivalves during the Paleocene?

````R
> N <- sum(BivalveAbundance["Paleocene",])
> n <- BivalveAbundance["Paleocene",]
> n <- n[which(n!=0)]
> -sum((n/N)*log(n/N))
[1] 4.511063
````

6) The percent change is (4.511063 - 5.086654)/5.086654  * 100% = -11.32% change

This negative change in the ShannonÕs Entropy reflects the mass extinction event at the Cretaceous-Paleogene boundary which led to the extinction of approximately 50% of bivalve genera. While this negative change is reflected in the index, the change is small compared to the actual magnitude of lost genera: this is because Shannon's Entropy is a flawed index which underrepresents richness changes which occur in different regions.

> Rather, it is a flawed index which overrepresents changes in evenness, as opposed to richness.

7)

````R
exp(ShannonÕs Entropy of Bivalves in the Late Cretaceous?)
> exp(5.086654)
 [1] 161.8474
exp(ShannonÕs Entropy of Bivalves during the Paleocene?)
> exp(4.511063)
[1] 91.01852
K-Pg percent change: (91.01852 - 161.8474)/ 161.8474 * 100% = -43.76% change
````

This much more accurately represents the magnitude of genera extinction at the K-Pg mass extinction: this number is much closer to the hypothesized 50% extinction.


## Problem Set 2

````R
1)
> specnumber(BivalveAbundance["Miocene",])
[1] 634
````

2)

````R
> diversity(BrachiopodAbundance["Late Ordovician",],index="simpson")
[1] 0.9784588
````

3) 

````R
> diversity(BivalveAbundance["Late Cretaceous",],index="shannon")
[1] 5.086512
````


4)

````R
> diversity(BivalveAbundance["Paleocene",],index="shannon")
[1] 4.511063
`````

## Problem Set 3

````R
> BrachRichness <- specnumber(BrachiopodAbundance)
> BivRichness <- specnumber(BivalveAbundance)

InOrderBrach <- BrachRichness[c("Early Ordovician","Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian","Middle Devonian","Late Devonian","Mississippian","Pennsylvanian","Cisuralian","Guadalupian","Lopingian","Early Triassic","Middle Triassic","Late Triassic","Early Jurassic","Middle Jurassic","Late Jurassic","Early Cretaceous","Late Cretaceous","Paleocene","Eocene","Oligocene","Miocene","Pliocene","Pleistocene")]
1)
> cor(InOrderBrach,InOrderBiv) 
[1] -0.567095
Brachiopod richness is negatively correlated with bivalve richness.
`````

2)

````R
> BrachRichnessSimp <- diversity(BrachiopodAbundance,index="simpson")
> BivRichnessSimp <- diversity(BivalveAbundance,index="simpson")

> cor(InOrderBrachSimp,InOrderBivSimp)
[1] -0.2355643
````

Still negatively correlated, but a weaker correlation.

3) The biggest drop in richness was between the epochs Lopingian and Early Triassic, corresponding to the Permo-Triassic mass extinction. The number of genera lost was 406-63 = 343 genera.

## Problem Set 4

1)

````R
> SampleAbundances<-apply(BrachiopodAbundance,1,sum)
> SampleAbundances[which(SampleAbundances==min(SampleAbundances))]
Pleistocene 
         63
> BrachStdRichness<-apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> BrachStdRichness[1:6]
    Mississippian     Pennsylvanian  Early Ordovician 
            42.67             34.18             38.08 
Middle Ordovician   Late Ordovician        Llandovery 
            46.21             42.02             41.19
````

2)

````R
> InOrderBrachStd <- BrachStdRichness[c("Early Ordovician","Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian","Middle Devonian","Late Devonian","Mississippian","Pennsylvanian","Cisuralian","Guadalupian","Lopingian","Early Triassic","Middle Triassic","Late Triassic","Early Jurassic","Middle Jurassic","Late Jurassic","Early Cretaceous","Late Cretaceous","Paleocene","Eocene","Oligocene","Miocene","Pliocene","Pleistocene")]
> BrachComp <- array(c(NA),dim=c(29,2))
> BrachComp[,1] <- InOrderBrach
> BrachComp[,2] <- InOrderBrachStd
> colnames(BrachComp) <- c("Non-Stnd","Stnd")
> BrachComp
      Non-Stnd  Stnd
 [1,]      141 	38.48
 [2,]      282 	46.39
 [3,]      331 	41.92
 [4,]      271 	41.65
 [5,]      257 	43.41
 [6,]      234 	43.99
 [7,]      138 	40.47
 [8,]      497 	49.73
 [9,]      353 	41.34
[10,]      274 	38.63
[11,]      314 	42.54
[12,]      284 	34.47
[13,]      564 	50.60
[14,]      549 	50.59
[15,]      406 	43.52
[16,]       63 	23.53
[17,]      111 	32.68
[18,]      193 	36.84
[19,]      130 	30.92
[20,]      175 	37.16
[21,]      111 	34.43
[22,]      125 	36.65
[23,]       96 	28.14
[24,]       29 	16.81
[25,]       57 	26.97
[26,]       30 	25.37
[27,]       45 	25.00
[28,]       23 	18.83
[29,]       19 	19.00
````

The standardized and non-standardized correspond fairly well, although the falls and rises in richness are greater in magnitude in the non-standardized richness measure.

3)
> plot(InOrderBrachStd,InOrderBivStd)

The two plots show similar results, with the scatterplots for standardized and non-standardized yield r-values of -0.545 and -0.567. The data show a linear negative correlation. The standardized plot exhibits a much more linear shape to the data, despite a wide spread of points, whereas the non-standardized plot approximates a hollow-curve plot. Although the data shapes are greatly changed the correlations remain relatively similar, so standardization is seemingly less important when comparing two standardized or non-standardized data sets among each other.

4) While I do think that the data and plots created do not rule out the possibility that bivalves outcompeted brachiopods, and in fact supports the hypothesis that bivalve richness increases over time as brachiopod richness decreases, I would be hesitant to accept the hypothesis that this trend is due to out-competition. Although the shift could reflect abiotic conditions changing and indirectly allowing bivalves to outcompete brachiopods, or even direct competition for resources, there is no further observations in this data set to support the claim. 

> Right on! Data Data Data!

Rather, it could be also explained as independent growth and declines for the classes, in which brachiopod niches decline over the Phanerozoic while a completely separate suite of niches for bivalves increase. Out-competition implies a common factor or variable in the respective richness evolutions, and since this is not implicit in the data I would not believe that this is evidence to accept the out-competition hypothesis.
