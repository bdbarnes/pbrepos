# Geosci 541 - Paleobiology
### 5/02/16
### Ben Davis Barnes

#### Problem Set 1

1)
````R
> counts_0<-count_uses(taxa[,"taxon_name"],0,pyr)
> counts_0 <- counts_0[order(-counts_0[,"matches"]),]
> counts_0[1:20,]
            string matches
10607         Lari      87
10574         Aves      18
3360         Acera       9
10969        Scopi       9
4020     Uncertain       8
3894     Ostracoda       4
8489       Bryozoa       4
3449     Crustacea       3
9694       Ariidae       3
3941    Healdiidae       2
13792   Pelmatozoa       2
14648      Metazoa       2
378        Insecta       1
397      Hemiptera       1
3458  Spinicaudata       1
3916    Cytheracea       1
3926    Cytheridae       1
3935    Bairdiacea       1
3939    Metacopina       1
3973    Bairdiidae       1
````

Lari corresponds to a suborder of waterbirds, such as gulls and small wading birds.
Aves is the class to which all birds belong.
Acera is a subclass of insects.
Scopi is a suborder of large bird.
Ostracoda is a class of small pelagic crustaceans.
Bryozoa is is a plylum of colonial marine invertebrates.
Crustacea is a subphylum of Arthropods including shelled invertebrates such as shrimp and crabs.
Ariidae is a family of catfish.
Healdiidae is a family of ostracods.
Pelmatozoa is an archaic classification of primitive echinoderms.
Metazoa is a kingdom classification of all animals.
Insecta is the class including all insects (fittingly enough).
Hemiptera is an order of Insecta including the confusingly named "true bugs."
Spinicaudata is an order of crustaceans known as "clam shrimp" with valves.
Cytheracea is a superfamily of ostracods.
Cytheridae is a family of ostracods.
Bairdiacea is a superfamily of ostracods.
Metacopina is a suborder of... what else, ostracods.
Bairdiidae is a family of ostracods.

Several of these taxa, particularly the first four, are poor data likely because they have such short names
