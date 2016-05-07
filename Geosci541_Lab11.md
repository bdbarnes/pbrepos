### Geosci 541 - Paleobiology
### Ben Barnes
### Lab 11 - 3/18/16

#### Problem Set 1

1)
````R
https://macrostrat.org/api/units?interval_name=Triassic&format=csv
TriassicUnits <- read.csv("~/Downloads/units.csv")
````

2)
````R
> length(unique(TriassicUnits[,"unit_id"]))
[1] 838
````

The dataset contains 838 Triassic units.

3)
````R
> TriassicUnits[1:10,]
````

Judging from the unit_name column, most of these units are igneous: volcanics and batholiths, or a metamorphic/igneous complex. These units would not be very relevent for an investigation of fossil preservation, since they will have not fossils preserved within them.

4)

The starting and ending ages of each unit are under the columns names "b_age" and "t_age", respectively.

5)

No; within the first ten units, most have b_ages corresponding to the Triassic, but a few begin around 396Ma (Devonian) and most of the units have a top age from the Cretaceous.

#### Problem Set 2

1)
````R
https://macrostrat.org/api/units?interval_name=Triassic&lith_class=sedimentary&format=csv
> TriassicUnits <- read.csv("~/Downloads/units (1).csv")
> dim(TriassicUnits)
[1] 713  17
````

2)
````R
> TriassicUnits <- subset(TriassicUnits,TriassicUnits[,"b_age"]<=252.17 & TriassicUnits[,"t_age"]>=201.3)
````

3)
````R
https://macrostrat.org/api/units?interval_name=Cretaceous&lith_class=sedimentary&format=csv
> CretaceousUnits <- read.csv("~/Downloads/units (3).csv")
> CretaceousUnits <- subset(CretaceousUnits,CretaceousUnits[,"b_age"]<= 145.0 & CretaceousUnits[,"t_age"]>=66.0)

https://macrostrat.org/api/units?interval_name=Cretaceous&lith_class=sedimentary&format=csv
> JurassicUnits <- read.csv("~/Downloads/units (4).csv")
> JurassicUnits <- subset(JurassicUnits,JurassicUnits[,"b_age"]<= 201.3 & JurassicUnits[,"t_age"]>=145.0)

https://macrostrat.org/api/units?interval_name=Permian&lith_class=sedimentary&format=csv
> PermianUnits <- read.csv("~/Downloads/units (5).csv")
> PermianUnits <- subset(PermianUnits,PermianUnits[,"b_age"]<= 298.9 & PermianUnits[,"t_age"]>=252.17)

https://macrostrat.org/api/units?interval_name=Carboniferous&lith_class=sedimentary&format=csv
> CarboniferousUnits <- read.csv("~/Downloads/units (6).csv")
> CarboniferousUnits <- subset(CarboniferousUnits,CarboniferousUnits[,"b_age"]<= 358.9 & CarboniferousUnits[,"t_age"]>=298.9)

https://macrostrat.org/api/units?interval_name=Devonian&lith_class=sedimentary&format=csv
> DevonianUnits <- read.csv("~/Downloads/units (7).csv")
> DevonianUnits <- subset(DevonianUnits,DevonianUnits[,"b_age"]<= 419.2 & DevonianUnits[,"t_age"]>=358.9)

https://macrostrat.org/api/units?interval_name=Silurian&lith_class=sedimentary&format=csv
> SilurianUnits <- read.csv("~/Downloads/units (8).csv")
> SilurianUnits <- subset(SilurianUnits,SilurianUnits[,"b_age"]<= 443.8 & SilurianUnits[,"t_age"]>= 419.2)

https://macrostrat.org/api/units?interval_name=Ordovician&lith_class=sedimentary&format=csv
> OrdovicianUnits <- read.csv("~/Downloads/units (9).csv")
> OrdovicianUnits <- subset(OrdovicianUnits,OrdovicianUnits[,"b_age"]<= 485.4 & OrdovicianUnits[,"t_age"]>= 443.8)
````

4)
````R
> UnitFreqs <- c(length(OrdovicianUnits[,1]),length(SilurianUnits[,1]),length(DevonianUnits[,1]),length(CarboniferousUnits[,1]),length(PermianUnits[,1]),length(TriassicUnits[,1]),length(JurassicUnits[,1]),length(CretaceousUnits[,1]))
````

5)
````R
> UnitFreqsNT <- subset(UnitFreqs,UnitFreqs!=604)
> mean(UnitFreqsNT)
[1] 1992.714
> sd(UnitFreqsNT)
[1] 1502.818
````

6)

No; the number of units for the Triassic (903) is within one standard deviation of the mean of the other periods, which doesn't make it too significantly different.

7)
````R
> UnitFreqsNTJ <- subset(UnitFreqsNT,UnitFreqsNT!=13)
> mean(UnitFreqsNTJ)
[1] 2322.667
> sd(UnitFreqsNTJ)
[1] 1340.022
````R

Now, both the numbers for the Triassic and Jurassic (903 and 13) are outside of one standard deviation from the mean. While this isn't that significant a distance, it does imply that these two data points are outliers to the rest.

#### Problem Set 3

1)
````R
> URL<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
> GotURL<-getURL(URL)
> PhanMap<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
> plot(PhanMap)

> URL<-"https://macrostrat.org/api/columns?format=geojson_bare&interval_name=Induan&Anisian&Olenekian&project_id=1"
> GotURL<-getURL(URL)
> TriasMap<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)

> plot(TriasMap,col="#B051A5")
````

2)
````R
> plot(PhanMap,ylim=range(0,90),xlim=range(-180,0))
> par(new=T)
> plot(TriasMap,col="#B051A5",ylim=range(0,90),xlim=range(-180,0))
````

3)
````R
> TriasFoss <- downloadPBDB(Taxa=c("Animalia"),StartInterval="Induan",StopInterval="Anisian")
> points(TriasFoss[,"lng"],TriasFoss[,"lat"],pch=19,ylim=range(0,90),xlim=range(-180,0))
````

4)
````R
> URL<-"https://macrostrat.org/api/columns?format=geojson_bare&interval_name=Lopingian&project_id=1"
> GotURL<-getURL(URL)
> LopMap<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
> plot(LopMap,col="#FBA794")
````

5)
````R
> LopFoss <- downloadPBDB(Taxa=c("Animalia"),StartInterval="Lopingian",StopInterval="Lopingian")
> points(LopFoss[,"paleolng"],LopFoss[,"paleolat"],pch=19,ylim=range(0,90),xlim=range(-180,0))
````

6)

Contrary to our initial hypothesis, the Macrostrat data shows a rise in areal extent of NA sedimentary rocks from the Lopingian to the Olenekian. The Triassic map shows almost all the same polygons preserved over the boundary, and several more included in the Triassic.

Again, contrary to our presumptions, the Triassic sedimentary record seems to have many more units with reported fossils than the Lopingian. While the Lopingian only has three or four recorded fossil occurrences in Macrostrat units, the Triassic 
Due to these two observations, and barring the realization that a mistake was made in the methods, I would reject the hypothesis that the Early Triassic diversity trough was due to poor fossil sampling or poor rock record. Both the fossil occurrences and rock units in the databases seem much better represented than in the Lopingian.
