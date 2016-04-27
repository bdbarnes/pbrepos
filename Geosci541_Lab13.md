# Geosci 541 - Paleobiology
### 4/25/16
### Ben Davis Barnes

#### Problem Set 1

1)

````R
> ncol(OrdovicianMatrix)
[1] 211
> ncol(SilurianMatrix)
[1] 423
````

These numbers of columns represent the number of genera present: the total generic diveristy is 211 and 423, respectively.
These numbers represent the **ADDITIVE** gamma diveristy.

2)

````R
> OrdoFrms <- rowSums(OrdovicianMatrix)
> mean(OrdoFrms)
[1] 26.60526

> SilFrms <- rowSums(SilurianMatrix)
> mean(SilFrms)
[1] 42.79167
````

These numbers represent the **ADDITIVE** alpha diveristy.

3)

Ordovician:
````R
> ncol(OrdovicianMatrix)-mean(OrdoFrms)
[1] 184.3947
````

Silurian:
````R
> ncol(SilurianMatrix)-mean(SilFrms)
[1] 380.2083
````
These numbers represent the **ADDITIVE** beta diveristy.

4)

````R
> mean(SilFrms)-mean(OrdoFrms)
[1] 16.1864
````

**ADDITIVE** alpha diveristy increases by 16.1864 into the Silurian.

````R
> (ncol(SilurianMatrix)-mean(SilFrms))-(ncol(OrdovicianMatrix)-mean(OrdoFrms))
[1] 195.8136
````

**ADDITIVE** beta diveristy increases by 195.8136 into the Silurian.

````R
> ncol(SilurianMatrix)-ncol(OrdovicianMatrix)
[1] 212
````

**ADDITIVE** gamma diveristy increases by 212 into the Silurian.

5)

**ADDITIVE** alpha diveristy percentages:
````R
> mean(OrdoFrms)/ncol(OrdovicianMatrix)
[1] 0.1260913
> mean(SilFrms)/ncol(SilurianMatrix)
[1] 0.1011623
````

**ADDITIVE** beta diveristy percentages:
````R
> (ncol(OrdovicianMatrix)-mean(OrdoFrms))/ncol(OrdovicianMatrix)
[1] 0.8739087
> (ncol(SilurianMatrix)-mean(SilFrms))/ncol(SilurianMatrix)
[1] 0.8988377
````

**ADDITIVE** beta diveristy percentages increase across the Ordo-Silurian boundary by 0.8988377-0.8739087 = 0.024929 or 2.49%
This indicates that in the Silurian the fauna became more distinct/diverse between communities, i.e. that the North American fauna became less cosmopolitan. This does not match what we learned in class, which was that following the Late Ordovician Mass Extinction fauna became significantly more cosmopolitan.

6)

One drawback of using percentages when comparing **ADDITIVE** alpha, **ADDITIVE** beta, and **ADDITIVE** gamma diveristies is that it does not communicate the magnitude of change. For example, the **ADDITIVE** beta diveristy change from the Ordovician to the Silurian, when reported as a percentage, sees only a 2.49% increase. However, the numerical change in **ADDITIVE** beta diveristy goes from ~184 to ~380, more than doubling the diveristy one would expect to find between communities. The same goes for the **ADDITIVE** alpha diveristy: decreasing by a mere 2.49% but in fact doubling from ~26.6 to ~42.8 from the Ordovician to the Silurian. The reported percentage change to these **ADDITIVE** diveristies understates the magnitude of these changes, when reported in relation to the total **ADDITIVE** gamma diveristy.

#### Problem Set 2

1)
````R
# Download data from the PBDB
> LatePermian<-downloadPBDB(Taxa="Animalia",StartInterval="Guadalupian",StopInterval="Lopingian")
> EarlyTriassic<-downloadPBDB(Taxa="Animalia",StartInterval="Induan",StopInterval="Ladinian")
> LateCretaceous<-downloadPBDB(Taxa="Animalia",StartInterval="Santonian",StopInterval="Maastrichtian")
> EarlyPaleogene<-downloadPBDB(Taxa="Animalia",StartInterval="Danian",StopInterval="Lutetian")

# Clean up bad genus names
> LatePermian<-cleanRank(LatePermian,"genus")
> EarlyTriassic <- cleanRank(EarlyTriassic,"genus")
> LateCretaceous <- cleanRank(LateCretaceous,"genus")
> EarlyPaleogene <- cleanRank(EarlyPaleogene,"genus")

# Constrain data to only occurrences limited to a single epoch
> LatePermian <- constrainAges(LatePermian,Epochs)
> EarlyTriassic <- constrainAges(EarlyTriassic,Epochs)
> LateCretaceous <- constrainAges(LateCretaceous,Epochs)
> EarlyPaleogene <- constrainAges(EarlyPaleogene,Epochs)

# Download stratigraphic unit information from the Macrostrat database and match it to the PBDB data
> LatePermian <- macrostratMatch(LatePermian)
> EarlyTriassic <- macrostratMatch(EarlyTriassic)
> LateCretaceous <- macrostratMatch(LateCretaceous)
> EarlyPaleogene <- macrostratMatch(EarlyPaleogene)

# Convert to community matrices
> PermianMatrix <- presenceMatrix(LatePermian,SampleDefinition="unit_name",TaxonRank="genus")
> TriassicMatrix <- presenceMatrix(EarlyTriassic,SampleDefinition="unit_name",TaxonRank="genus")
> CretaceousMatrix <- presenceMatrix(LateCretaceous,SampleDefinition="unit_name",TaxonRank="genus")
> PaleogeneMatrix <- presenceMatrix(EarlyPaleogene,SampleDefinition="unit_name",TaxonRank="genus")

# Cull the matrices
> PermianMatrix<-cullMatrix(PermianMatrix,2,10)
> TriassicMatrix<-cullMatrix(TriassicMatrix,2,10)
> CretaceousMatrix<-cullMatrix(CretaceousMatrix,2,10)
> PaleogeneMatrix<-cullMatrix(PaleogeneMatrix,2,10)

