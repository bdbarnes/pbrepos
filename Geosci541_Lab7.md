Geosci 541 Ð Paleobiology
Lab Exercise #7 (3/07/16)
Ben Davis Barnes
Problem Set 1

> 20/20

1)
	max_ma and min_ma represent the oldest and youngest occurrence age, respectively, in units of millions of years (i.e. Ma).

2)

````R
> DataPBDBMaxMA <- tapply(DataPBDB$max_ma,DataPBDB$genus,max)
> DataPBDBMaxMA[1:5]
         Abra   Abrachlamys Acanthocardia          Acar 
        56.00         23.03         66.00         66.00 
       Acesta 
        66.00
````

3)
````R
> DataPBDBMinMA <- tapply(DataPBDB$min_ma,DataPBDB$genus,min)
> DataPBDBMinMA[1:5]
         Abra   Abrachlamys Acanthocardia          Acar 
       0.0000       15.9700        0.0000        0.0000 
       Acesta 
       0.0117	
````

4)

````R
> sort(table(DataPBDB[,"genus"]))
[1] Anadara 1916
````

5)
> DataPBDBAnadara <- subset(DataPBDB,DataPBDB[,"genus"]=="Anadara")
> max(DataPBDBAnadara[,"max_ma"])
[1] 66
> min(DataPBDBAnadara[,"min_ma"])
[1] 0

Problem Set 2
1)

````R
mean() finds the arithmetic mean of the vector
sample() takes a sample from the specified data:
	x, the first argument, specifies the data to sample
	length() specifies the size of the sample to be taken
		(in this case, the same as the vector length)
	replace=TRUE, meaning that after sample n ,sample n+1 will not be 		drawing from the total data except for n: replacement of 			data occurs
````

2)

````R
> plot(density(ResampledMeans))
The density plot adopts an approximately symmetrical bell curve, but with a much more narrow distribution (very narrow range). However, in general I would call it to a Gaussian distribution.
````

3)

````R
> mean(ResampledMeans)
[1] 24.16008
This is very close to the original mean of 24.1997.
````

4)

````R
> sort(ResampledMeans)
````

5)

````R
> quantile(ResampledMeans,c(.025,.975))
    2.5%    97.5% 
21.82094 26.28630
````

6)

These two numbers are the upper and lower confidence interval because they encompass the middle 95% of our computed means: any values in the lower 2.5% or upper 97.5% are outside, and correspond to the probability of 0.05 that the value of our parameter lies outside of the confidence interval.


## Problem Set 3

1)
I think it is likely that *Lucina* is still alive.

2)
> Dallarca <- subset(DataPBDB,DataPBDB[,"genus"]=="Dallarca")
> estimateExtinction(Dallarca[,"min_ma"],0.95)
Earliest   Latest 
 2.58800 -3.88749
````

3) Based on the 95% confidence interval, I would say that it is likely that Dallarca is alive today the lower bound of the confidence interval being negative indicates it is within the realm of probability that it is extant.

4)
Based on this case, it is clear that we cannot always trust confidence intervals, since they produce estimates of probable ranges which are statistically robust but don't match up with fossil evidence.

## Problem Set 4

1) Populations of species and genera do not stay constant: they wane and wax, growing and shrinking and dividing. For this ecological reason, it is unlikely that even a well-constrained stratigraphic lifespan of a taxon would feature random distribution.

2) A random distribution of fossil species during their species lifespan necessitates no preferential preservation or destruction in the rock record, that each fossil should be equally likely to occur in any rock unit. This we know not to be true: certain fragile or small taxa are preferentially destroyed from the geologic record, and diagenesis can introduce a huge bias in a nonrandom fashion when it occurs within one unit but not another, depending on environmental factors or chance.

## Problem Set 5
1)
````R
> dim(DataPBDB)
[1] 67617    26
> dim(ExtantData)
[1] 59096    26
Thus, we lost 67617-59096 = 8521 occurrences
````

2)
````R
> length(unique(DataPBDB[,"genus"]))
[1] 1018
> length(unique(ExtantData[,"genus"]))
[1] 532
Percent of extant Cenozoic bivalve genera today:
	532/1018 * 100 = 52.26%
````

3)
````R
> ExtantMaxMA <- tapply(ExtantData$max_ma,ExtantData$genus,max)
> ExtantMinMA <- tapply(ExtantData$min_ma,ExtantData$genus,min)
> ExtantStratRanges <- matrix(c(NA),nrow=length(ExtantMaxMA),ncol=2)
> colnames(ExtantStratRanges) <- c("Max","Min")
> ExtantStratRanges[,1] <- ExtantMaxMA
> ExtantStratRanges[,2] <- ExtantMinMA
> rownames(ExtantStratRanges) <- rownames(ExtantMinMA)
> ExtantStratRanges[1:5,]
               Max    Min
Abra          56.0 0.0000
Acanthocardia 66.0 0.0000
Acar          66.0 0.0000
Acesta        66.0 0.0117
Acharax       48.6 2.5880
````

4)
````R
> which(ExtantStratRanges[,2]!=0.0000)
[1] too many to copy here
````

5)
````R
> Scrobicularia <- subset(DataPBDB,DataPBDB[,"genus"]=="Scrobicularia")
> estimateExtinction(Scrobicularia[,"min_ma"],0.95)
 Earliest    Latest 
  0.01170 -34.70966
and so onÉ
> GeneraStratRange
              Earliest      Latest
Scrobicularia   0.0117 -34.7096595
Meiocardia      0.0117  -5.3295740
Dimya           0.7810  -2.0546884
Digitaria       0.7810  -3.7611543
Cuspidaria      2.5880   0.7771965
Arctica         0.0117  -1.7991035
Aloides         5.3330        -Inf
Kurtiella       0.0117 -34.7096595
Gouldia         0.0117  -2.0473855
Acrosterigma    0.0117  -3.4811285
````

8/10 of the genera have lower bounds of their minimum age confidence intervals in the negatives, indicating that the use of confidence intervals has yielded a 95% probability of the data being explained by them being extant. One genus, Aloides, did not have more than one datum and so a confidence interval could not be reproduced for it, although the min age indicated (5.333Ma) does not indicate that we could hypothesize it is extant just from looking at the data.
