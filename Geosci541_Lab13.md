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

