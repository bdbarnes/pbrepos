Geosci 541 Ð Paleobiology
Lab Exercise 4 (2/15/16)
Ben Davis Barnes

20/20

## Problem Set I

1) There are 602 genera in the Miocene, 169 genera in the Early Jurassic, 375 genera in the Late Cretaceous, and 133 taxa in the Pennsylvanian. This was found through:
	
````R
>list(sum(PresencePBDB["Miocene",]),sum(PresencePBDB["Early Jurassic",]),sum(PresencePBDB["Late Cretaceous",]),sum(PresencePBDB["Pennsylvanian",]))
````

2)
````R
>nrow(PresencePBDB)	[1] 29
````
3) 

````R
>list(c=which(PresencePBDB[,ÓMytilusÓ]==1)) (# = 17)
````

Pridoli, Early Devonian, Cisuralian, Early Triassic, Middle Triassic, Late Triassic, Early Jurassic, Middle Jurassic, Late Jurassic, Early Cretaceous, Late Cretaceous, Paleocene, Eocene, Oligocene, Miocene, Pliocene, Pleistocene

4) If we assume that Mytilus is present in the geologic history even if no fossil occurrence is recorded during the intervals between epochs during which it is recorded as existing, we can infer that the genus was alive also during:

Middle Devonian, Upper Devonian, Mississippian, Pennsylvanian, Guadalupian, and Lopingian.


## Problem Set II

1) 

````R
Jaccard <-  function(Sample1, Sample2){
 	    VectorA <- names(which(PresencePBDB[Sample1,]==1))
   	  VectorB <- names(which(PresencePBDB[Sample2,]==1))
 	    VectorC <- c(VectorA,VectorB)
 	    JI <- ((length(intersect(VectorA,VectorB)))/(length(unique(VectorC))))
 	    return(JI)
       }
       
>Jaccard("Miocene","Pleistocene")
[1] 0.8279221
````

2)

````R
> Jaccarddist <-  function(Sample1, Sample2){
 	  VectorA <- names(which(PresencePBDB[Sample1,]==1))
 	  VectorB <- names(which(PresencePBDB[Sample2,]==1))
 	  VectorC <- c(VectorA,VectorB)
 	  JDI <- 1-((length(intersect(VectorA,VectorB)))/(length(unique(VectorC))))
   	return(JDI)
    }

>Jaccarddist(ÒMioceneÓ,ÓPleistoceneÓ)
[1] 0.1720779
````

3)

````R
>vegdist(PresencePBDB,method=ÓjaccardÓ)
[1] 0.17207791
````

4) 

````R
> vegdist(PresencePBDB[c("Pleistocene","Pliocene","Miocene","Oligocene","Eocene","Paleocene"),])
````

The two most dissimilar epochs (that is, the most distant) are, unsurprisingly, the Paleocene and Pleistocene (distance = 0.28571429).

> Are you sure that's the correct number?

## Problem Set III

1)
````R
> RandomEpochs <- PresencePBDB[c("Pliocene","Oligocene","Paleocene","Early Cretaceous","Late Jurassic","Middle Jurassic"),]
````

2)
````R
> vegdist(RandomEpochs)
                   Pliocene      Oligocene      Paleocene      Early Cret. 	L. Jurassic
Oligocene   0.1047794                    
Paleocene   0.2339181   0.2581967          
Early Cret.  0.5952663   0.5974843    0.4706685
L. Jurassic   0.7625330   0.7627119    0.6532508     0.3075269              
M. Jurassic  0.7941176   0.7879656    0.6572327     0.3230769        0.1739130
````

3) The most dissimilar epochs are the Middle Jurassic and the Pliocene (0.7941176)
	Middle Jurassic (0 // 1)
	     - L. Jurassic (0.174 // 0.763)
	     - Early Cret. (0.323 // 0.595)
	     - Paleocene (0.657 // 0.234)
	     - Oligocene (0.788 // 0.105)
	Pliocene (1 // 0)

4) The variable which controls the distance of each epoch in regards to these two poles is proximity the geologic time scale. The ordination matches perfectly the chronologic order of those epochs in the geologic time scale, and the epochs from the Mesozoic (Middle Jurassic, Late Jurassic, and Early Cretaceous) are much closer to each other and more distant from the Cenozoic Paleocene, Oligocene, and Pliocene, and vice versa.

5) Although the Early Cretaceous and the Paleocene are not too temporally distant, separated by a mere ~50 million years, their relatively high dissimilarity may be due to the mass extinction at the Cretaceous-Paleogene boundary which would have caused the extinction of many genera of bivalves and gastropods and allowed for the origination of new species in the Paleocene.

## Problem Set IV

1)
````R
> Ordovician <-downloadPBDB(Taxa="Animalia",StartInterval="Ordovician",StopInterval="Ordovician")
````

2)
````R
> Ordovician <- cleanGenus(Ordovician)
````

3)
````R
> OrdovicianComm <- presenceMatrix(Ordovician,SampleDefinition="geoplate")
> OrdovicianComm<-cullMatrix(OrdovicianComm,minOccurrences=2,minDiversity=25)
````

4)
Having searched and searched for a pattern along the axes corresponding to lat/long coordinates of the geoplates, I have concluded that there is no clear relationship. The code used was:

````R
> plot(OrdoDCA,display=ÒsitesÓ)
> mean(Ordovician[which(Ordovician[,"geoplate"]==XXX),"paleolng"])
> mean(Ordovician[which(Ordovician[,"geoplate"]==XXX),"paleolat"])
````

These averaged coordinates were then compared on the DCA plot to search for a gradient or directional relationship. Although plates located further to the right on the DCA1 axis were more likely to have a negative latitude, there were exceptions (plate 0) just as plates to the left were not always located at positive latitudes (plate 611, for example). Without a clear relationship, I was forced to conclude that the distance along axes and away from other points signaled instead heterogeneity of the sample data, such as variance, or in general significant differences.


