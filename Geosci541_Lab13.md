# Geosci 541 - Paleobiology
### 4/25/16
### Ben Davis Barnes

#### Problem Set 1

1)

````R
> dim(OrdovicianMatrix)
[1] 45 23
> dim(SilurianMatrix)
[1] 68 53
````

This second dimension representing the number of genera present, the total generic diversity is 23 and 52, respectively.
These numbers rempresent the ADDITIVE gamma diversity.

2)

````R
> OrdoFrms <- rowSums(OrdovicianMatrix)
> mean(OrdoFrms)
[1] 7.688889

> SilFrms <- rowSums(SilurianMatrix)
> mean(SilFrms)
[1] 11.57353
````

These numbers represent the ADDITIVE alpha diversity.

3)

Ordovician:
````R
> 23 - mean(OrdoFrms)
[1] 15.31111
````

Silurian:
````R
> 52 - mean(SilFrms)
[1] 40.42647
````
These numbers represent the ADDITIVE beta diversity.

