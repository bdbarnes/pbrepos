# Geosci 541 - Paleobiology
### 5/02/16
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
````

2)

Gamma diveristies:
````R
> ncol(PermianMatrix)
[1] 311

> ncol(TriassicMatrix)
[1] 158

> ncol(CretaceousMatrix)
[1] 774

> ncol(PaleogeneMatrix)
[1] 1031
````

Alpha diveristies:
````R
> PermFrms <- rowSums(PermianMatrix)
> mean(PermFrms)
[1] 57.63636

> TriFrms <- rowSums(TriassicMatrix)
> mean(TriFrms)
[1] 35.15385

> KFrms <- rowSums(CretaceousMatrix)
> mean(KFrms)
[1] 57.90625

> PalFrms <- rowSums(PaleogeneMatrix)
> mean(PalFrms)
[1] 52.83333
````

Beta diveristies:
````R
> ncol(PermianMatrix)-mean(PermFrms)
[1] 253.3636

> ncol(TriassicMatrix)-mean(TriFrms)
[1] 122.8462

> ncol(CretaceousMatrix)-mean(KFrms)
[1] 716.0938

> ncol(PaleogeneMatrix)-mean(PalFrms)
[1] 978.1667
````

3)

Alpha diveristies as a percentage:
````R
> mean(PermFrms)/ncol(PermianMatrix)
[1] 0.1853259

> mean(TriFrms)/ncol(TriassicMatrix)
[1] 0.2224927

> mean(KFrms)/ncol(CretaceousMatrix)
[1] 0.07481428

> mean(PalFrms)/ncol(PaleogeneMatrix)
[1] 0.05124475
````

Beta diveristies as a percentage:
````R
> 1-mean(PermFrms)/ncol(PermianMatrix)
[1] 0.8146741

> 1-mean(TriFrms)/ncol(TriassicMatrix)
[1] 0.7775073

> 1-mean(KFrms)/ncol(CretaceousMatrix)
[1] 0.9251857

> 1-mean(PalFrms)/ncol(PaleogeneMatrix)
[1] 0.9487553
````

4)

Alpha biodiveristy changes:
````R
> mean(TriFrms)-mean(PermFrms)
[1] -22.48252

> mean(PalFrms)-mean(KFrms)
[1] -5.072917
````
The alpha diveristy decreases a lot across the Permo-Triassic boundary, and decreases moderately through the KT event.

5)

Alpha biodiveristy percentage changes:
````R
> (mean(TriFrms)/ncol(TriassicMatrix))-(mean(PermFrms)/ncol(PermianMatrix))
[1] 0.03716677

> (mean(PalFrms)/ncol(PaleogeneMatrix))-mean(KFrms)/ncol(CretaceousMatrix)
[1] -0.02356953
````
The alpha diveristy increases slightly across the Permo-Triassic ME, but decreases slightly through the KT event.


#### Problem Set 3

1)
````R
# Download data from the PBDB
> LateOrdovician<-downloadPBDB(Taxa="Animalia",StartInterval="Sandbian",StopInterval="Hirnantian")
> EarlySilurian<-downloadPBDB(Taxa="Animalia",StartInterval="Llandovery",StopInterval="Wenlock")

# Clean up bad genus names
> LateOrdovician<-cleanRank(LateOrdovician,"genus")
> EarlySilurian <- cleanRank(EarlySilurian,"genus")

# Constrain data to only occurrences limited to a single epoch
> LateOrdovician <- constrainAges(LateOrdovician,Epochs)
> EarlySilurian <- constrainAges(EarlySilurian,Epochs)

# Download stratigraphic unit information from the Macrostrat database and match it to the PBDB data
> LateOrdovician <- macrostratMatch(LateOrdovician)
> EarlySilurian <- macrostratMatch(EarlySilurian)

# Convert to abundance matrices
> OrdovicianMatrix <- abundanceMatrix(LateOrdovician,SampleDefinition="unit_name",TaxonRank="genus")
> SilurianMatrix <- abundanceMatrix(EarlySilurian,SampleDefinition="unit_name",TaxonRank="genus")
> PermianMatrix <- abundanceMatrix(LatePermian,SampleDefinition="unit_name",TaxonRank="genus")
> TriassicMatrix <- abundanceMatrix(EarlyTriassic,SampleDefinition="unit_name",TaxonRank="genus")
> CretaceousMatrix <- abundanceMatrix(LateCretaceous,SampleDefinition="unit_name",TaxonRank="genus")
> PaleogeneMatrix <- abundanceMatrix(EarlyPaleogene,SampleDefinition="unit_name",TaxonRank="genus")

# Cull the matrices
> OrdovicianMatrix<-cullMatrix(OrdovicianMatrix,2,10)
> SilurianMatrix<-cullMatrix(SilurianMatrix,2,10)
> PermianMatrix<-cullMatrix(PermianMatrix,2,10)
> TriassicMatrix<-cullMatrix(TriassicMatrix,2,10)
> CretaceousMatrix<-cullMatrix(CretaceousMatrix,2,10)
> PaleogeneMatrix<-cullMatrix(PaleogeneMatrix,2,10)
````

2)

Gamma diveristies:
````R
> OrdSums <- colSums(OrdovicianMatrix)
> exp(diversity(OrdSums,index="shannon"))
[1] 67.6812

> SilSums <- colSums(SilurianMatrix)
> exp(diversity(SilSums,index="shannon"))
[1] 207.7563

> PermSums <- colSums(PermianMatrix)
> exp(diversity(PermSums,index="shannon"))
[1] 149.5363

> TriSums <- colSums(TriassicMatrix)
> exp(diversity(TriSums,index="shannon"))
[1] 96.54487

> KSums <- colSums(CretaceousMatrix)
> exp(diversity(KSums,index="shannon"))
[1] 309.0791

> PalSums <- colSums(PaleogeneMatrix)
> exp(diversity(PalSums,index="shannon"))
[1] 396.4146
````

Alpha diveristies:
````R
> exp(mean(diversity(OrdovicianMatrix,index="shannon")))
[1] 16.03987

> exp(mean(diversity(SilurianMatrix,index="shannon")))
[1] 24.88629

> exp(mean(diversity(PermianMatrix,index="shannon")))
[1] 27.41836

> exp(mean(diversity(TriassicMatrix,index="shannon")))
[1] 19.33984

> exp(mean(diversity(CretaceousMatrix,index="shannon")))
[1] 27.6654

> exp(mean(diversity(PaleogeneMatrix,index="shannon")))
[1] 31.90602
````

Beta diveristies:
````R
> (exp(diversity(OrdSums,index="shannon")))-(exp(mean(diversity(OrdovicianMatrix,index="shannon"))))
[1] 51.64133

> (exp(diversity(SilSums,index="shannon")))-(exp(mean(diversity(SilurianMatrix,index="shannon"))))
[1] 182.87

> (exp(diversity(PermSums,index="shannon")))-(exp(mean(diversity(PermianMatrix,index="shannon"))))
[1] 122.118

> (exp(diversity(TriSums,index="shannon")))-(exp(mean(diversity(TriassicMatrix,index="shannon"))))
[1] 77.20503

> (exp(diversity(KSums,index="shannon")))-(exp(mean(diversity(CretaceousMatrix,index="shannon"))))
[1] 281.4137

> (exp(diversity(PalSums,index="shannon")))-(exp(mean(diversity(PaleogeneMatrix,index="shannon"))))
[1] 364.5086
````

3)

Alpha diveristy as a percentage of Gamma:
````R
> exp(mean(diversity(OrdovicianMatrix,index="shannon")))/exp(diversity(OrdSums,index="shannon"))
[1] 0.2369916

> exp(mean(diversity(SilurianMatrix,index="shannon")))/exp(diversity(SilSums,index="shannon"))
[1] 0.119786

> exp(mean(diversity(PermianMatrix,index="shannon")))/exp(diversity(PermSums,index="shannon"))
[1] 0.1833559

> exp(mean(diversity(TriassicMatrix,index="shannon")))/exp(diversity(TriSums,index="shannon"))
[1] 0.2003197

> exp(mean(diversity(CretaceousMatrix,index="shannon")))/exp(diversity(KSums,index="shannon"))
[1] 0.08950913

> exp(mean(diversity(PaleogeneMatrix,index="shannon")))/exp(diversity(PalSums,index="shannon"))
[1] 0.08048647
````

Beta diveristy as a percentage of Gamma:
````R
> 1-exp(mean(diversity(OrdovicianMatrix,index="shannon")))/exp(diversity(OrdSums,index="shannon"))
[1] 0.7630084

> 1-exp(mean(diversity(SilurianMatrix,index="shannon")))/exp(diversity(SilSums,index="shannon"))
[1] 0.880214

> 1-exp(mean(diversity(PermianMatrix,index="shannon")))/exp(diversity(PermSums,index="shannon"))
[1] 0.8166441

> 1-exp(mean(diversity(TriassicMatrix,index="shannon")))/exp(diversity(TriSums,index="shannon"))
[1] 0.7996803

> 1-exp(mean(diversity(CretaceousMatrix,index="shannon")))/exp(diversity(KSums,index="shannon"))
[1] 0.9104909

> 1-exp(mean(diversity(PaleogeneMatrix,index="shannon")))/exp(diversity(PalSums,index="shannon"))
[1] 0.9195135
````

Gamma diveristy as a percentage of Gamma:
````R
> exp(diversity(OrdSums,index="shannon"))/exp(diversity(OrdSums,index="shannon"))
[1] 1

> exp(diversity(SilSums,index="shannon"))/exp(diversity(SilSums,index="shannon"))
[1] 1

> exp(diversity(PermSums,index="shannon"))/exp(diversity(PermSums,index="shannon"))
[1] 1

> exp(diversity(TriSums,index="shannon"))/exp(diversity(TriSums,index="shannon"))
[1] 1

> exp(diversity(KSums,index="shannon"))/exp(diversity(KSums,index="shannon"))
[1] 1

> exp(diversity(PalSums,index="shannon"))/exp(diversity(PalSums,index="shannon"))
[1] 1
````

4)

Alpha biodiveristy change:
````R
> (exp(mean(diversity(SilurianMatrix,index="shannon"))))-(exp(mean(diversity(OrdovicianMatrix,index="shannon"))))
[1] 8.846421

> (exp(mean(diversity(TriassicMatrix,index="shannon"))))-(exp(mean(diversity(PermianMatrix,index="shannon"))))
[1] -8.078527

> (exp(mean(diversity(PaleogeneMatrix,index="shannon"))))-(exp(mean(diversity(CretaceousMatrix,index="shannon"))))
[1] 4.24062
````

5)

Alpha biodiveristy change as a percentage of Gamma:
````R
> (exp(mean(diversity(SilurianMatrix,index="shannon")))/exp(diversity(SilSums,index="shannon")))-(exp(mean(diversity(OrdovicianMatrix,index="shannon")))/exp(diversity(OrdSums,index="shannon")))
[1] -0.1172055

> (exp(mean(diversity(TriassicMatrix,index="shannon")))/exp(diversity(TriSums,index="shannon")))-(exp(mean(diversity(PermianMatrix,index="shannon")))/exp(diversity(PermSums,index="shannon")))
[1] 0.01696379

> (exp(mean(diversity(PaleogeneMatrix,index="shannon")))/exp(diversity(PalSums,index="shannon")))-(exp(mean(diversity(CretaceousMatrix,index="shannon")))/exp(diversity(KSums,index="shannon")))
[1] -0.009022655
````

#### Problem Set 4

Problem Set 1 showed a slight percentage increase of beta diveristy from the Ordovician to the Silurian. Problem Set 2 showed a decrease through the Permo-Triassic and an increase through the KT for beta diveristy. Finally, in Problem Set 3 using Shanon's exponentiated Entropy's beta diveristy estimates, it increased through the Ordo-Silurian and KT, but decreased through the Permo-Triassic. Based on these results, and knowing that the Permo-Triassic represents the most devastatingly global mass extinction and thus may be an exception, I would hypothesize that beta diveristy tends to increase slightly through mass extinction events: I posit that this process occurs because the global nature of the kill mechanisms affect each community worldwide, but do not necessarily select against the same species in each community, leading to a net intrercommunity diversification. However, the caluclations from this data set do not suggest a particularly significant beta diveristy increase, and so more analysis will have to be done to get a clear picture of these patterns.
