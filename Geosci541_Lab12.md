### Geosci 541 - Paleobiology
### Ben Davis Barnes

### Lab 12 - 3/18/16

> 18/20

#### Problem Set 1

1)
````R
> TriassicSynapsids <- downloadPBDB("Synapsida","Anisian","Rhaetian")
> TriassicSynapsids <- cleanRank(TriassicSynapsids,"genus")
> TriassicDiapsids <- downloadPBDB("Diapsida","Anisian","Rhaetian")
> TriassicDiapsids <- cleanRank(TriassicDiapsids,"genus")
> JurassicDiapsids <- downloadPBDB("Diapsida","Hettangian","Tithonian")
> JurassicDiapsids <- cleanRank(JurassicDiapsids,"genus")
> JurassicSynapsids <- downloadPBDB("Synapsida","Hettangian","Tithonian")
> JurassicSynapsids <- cleanRank(JurassicSynapsids,"genus")
````

2)
````R
> length(unique(TriassicDiapsids[,"genus"]))
[1] 389
> length(unique(TriassicSynapsids[,"genus"]))
[1] 116
````

3)
````R
> DiapsidSurvivors <- intersect(TriassicDiapsids[,"genus"],unique(JurassicDiapsids[,"genus"]))
> length(DiapsidSurvivors)
[1] 32

> DiapsidVictims <- setdiff(TriassicDiapsids[,"genus"],unique(JurassicDiapsids[,"genus"]))
> length(DiapsidVictims)
[1] 357

> SynapsidSurvivors <- intersect(TriassicSynapsids[,"genus"],unique(JurassicSynapsids[,"genus"]))
> length(SynapsidSurvivors)
[1] 8

> SynapsidVictims <- setdiff(TriassicSynapsids[,"genus"],unique(JurassicSynapsids[,"genus"]))
> length(SynapsidVictims)
[1] 108
````

4)
````R
> TotalDiapsids <- c(TriassicDiapsids[,"genus"],JurassicDiapsids[,"genus"])
> length(unique(TotalDiapsids))
[1] 874

> TotalSynapsids <- c(TriassicSynapsids[,"genus"],JurassicSynapsids[,"genus"])
> length(unique(TotalSynapsids))
[1] 254

> DiapsidOdds<- (length(DiapsidSurvivors)/length(unique(TotalDiapsids))) / (length(DiapsidVictims)/length(unique(TotalDiapsids)))
> DiapsidOdds
[1] 0.08963585

> SynapsidOdds<- (length(SynapsidSurvivors)/length(unique(TotalSynapsids))) / (length(SynapsidVictims)/length(unique(TotalSynapsids)))
> SynapsidOdds
[1] 0.07407407

> OddsidRatio <- DiapsidOdds/SynapsidOdds
> OddsidRatio
[1] 1.210084

> log(OddsidRatio)
[1] 0.1906898
````

5)
````R
> SEsid <- sqrt(1/length(SynapsidSurvivors) + 1/length(SynapsidVictims) + 1/length(DiapsidSurvivors) + 1/length(DiapsidVictims))
> SEsid
[1] 0.4102565

> UpperLimitsid <- log(OddsidRatio) + (SEsid*1.96)
> UpperLimitsid
[1] 0.9947925

> LowerLimitsid <- log(OddsidRatio) - (SEsid*1.96)
> LowerLimitsid
[1] -0.6134129
````

Because this 95% confidence interval includes negative values within its lower bounds, we cannot say that our positive log-odds results are statistically significant.

#### Problem Set 2

1)
````R
> TriassicApsids <- downloadPBDB(c("Synapsida","Diapsida"),"Anisian","Rhaetian")
> TriassicApsids <- cleanRank(TriassicApsids,"genus")
> PostTriassicApsids <- downloadPBDB(c("Synapsida","Diapsida"),"Hettangian","Cenozoic")
> PostTriassicApsids <- cleanRank(PostTriassicApsids,"genus")
````

2)
````R
> mean(TriassicApsids[,"paleolat"])
[1] 6.709582

> TriasLat <- tapply(TriassicApsids[,"paleolat"],TriassicApsids[,"genus"],mean)
````

3)
````R
> TriassicSurvivors <- subset(TriassicApsids,TriassicApsids[,"genus"]%in%unique(PostTriassicApsids[,"genus"])==TRUE)
> TriassicSurvivors <- unique(TriassicSurvivors[,"genus"])

> TriassicVictims <- subset(TriassicApsids,TriassicApsids[,"genus"]%in%unique(PostTriassicApsids[,"genus"])!=TRUE)
> TriassicVictims <- unique(TriassicVictims[,"genus"])
````

4)
````R
> TriassicApsidsDi <- subset(TriassicApsids,TriassicApsids[,"genus"]%in%unique(TriassicDiapsids[,"genus"])==TRUE)
> TriassicApsidsSyn <- subset(TriassicApsids,TriassicApsids[,"genus"]%in%unique(TriassicSynapsids[,"genus"])==TRUE)
````

5)
````R
> MeanLats <- tapply(TriassicApsids[,"paleolat"],TriassicApsids[,"genus"],mean)
> head(MeanLats)
 Acaenasuchus  Acallosuchus Acompsosaurus   Actiosaurus Adamanasuchus 
   0.116        10.430        10.740        32.120        10.145 
Adelobasileus 
  10.170 

> PTVictims <- array(0,dim=length(TriassicVictims),dimnames=list(TriassicVictims))

> FinalMatrix <- merge(MeanLats,PTVictims,all=TRUE,by="row.names")
> head(FinalMatrix)
      Row.names      x y
1  Acaenasuchus 10.116 0
2  Acallosuchus 10.430 0
3 Acompsosaurus 10.740 0
4   Actiosaurus 32.120 0
5 Adamanasuchus 10.145 0
6 Adelobasileus 10.170 0

> FinalMatrix <- transform(FinalMatrix,row.names=Row.names,Row.names=NULL)
> colnames(FinalMatrix) <- c("MeanLatitudes","Survivor/Victim")
> head(FinalMatrix)
              MeanLatitudes Survivor/Victim
Acaenasuchus         10.116               0
Acallosuchus         10.430               0
Acompsosaurus        10.740               0
Actiosaurus          32.120               0
Adamanasuchus        10.145               0
Adelobasileus        10.170               0

> FinalMatrix[is.na(FinalMatrix[,"Survivor/Victim"]),] <- 1

> Regression<-glm(FinalMatrix[,"Survivor/Victim"]~FinalMatrix[,"MeanLatitudes"],family="binomial")

> summary(Regression)

Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[, 
    "MeanLatitudes"], family = "binomial")

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-0.4529  -0.4466  -0.4440  -0.4362   2.1782  

Coefficients:
                                 Estimate Std. Error z value Pr(>|z|)
(Intercept)                    -2.2750384  0.1532604  -14.84   <2e-16
FinalMatrix[, "MeanLatitudes"]  0.0007675  0.0051136    0.15    0.881
                                  
(Intercept)                    ***
FinalMatrix[, "MeanLatitudes"]    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 312.48  on 503  degrees of freedom
Residual deviance: 312.46  on 502  degrees of freedom
AIC: 316.46

Number of Fisher Scoring iterations: 5

````
Mean latitude was **not** a very good predictor of survivorship through the mass extinction: the estimate of the slope of the regression line was 0.0007675, which is a very small slope and smaller than the standard error associated with it. It is unlikely that the data shows a strong relationship between survivorship and living at higher latitudes.


> You didn't do the last question!


