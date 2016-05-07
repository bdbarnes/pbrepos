### Geosci 541 - Paleobiology
### Ben Davis Barnes

### Lab 12 - 3/18/16

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

