Geosci 541 – Paleobiology
Lab Exercise #8 (3/28/16)
Ben Davis Barnes
Problem Set 1

1) Modern-day North America lies to the west of its Cretaceous position.

2) plot() is a function which produces a plot. The first argument identifies the source of data, col= indicates the rgb color setting to be used (red, green, blue vectors, and alpha transparency), lty= indicates the line type to be used (different gradients of solid or dashed patterns), and add=TRUE indicates that the modern map should be added to the existing plot.

4)
> AlbianMap <- downloadPaleogeography(Age=110)
> plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0.01,add=TRUE)

5) Since the Albian, the Eurasian continent has generally moved south, while Africa, India, and Australia have generally moved north-east (particularly the Indian subcontinent and Australia).

6) Since the Albian, the North and South American continents have moved dramatically west.

Problem Set 2

1)
> plot(PEMap,col=rgb(0,.66,.33,0.33),lty=0.01)

2)
> Anthozoa<-downloadPBDB(Taxa=c("Anthozoa"),StartInterval="Paleocene",StopInterval="Eocene")

3)
> dim(Anthozoa)
[1] 2847   26
There are 2847 occurrences.

4)
> colnames(Anthozoa)
 + "occurrence_no" = reference number of that occurrence
 + "record_type" = the type of record (all "occurrences")
 + "reid_no" = record ID number
 + "flags" = whether this is a flagged occurrence      
 + "collection_no" = reference number of the collection from which this occurrence is drawn
 + "identified_name" = the taxonomic name under which the occurrence has been identified
 + "identified_rank" = the taxonomic rank of the above name (genus, sp., etc.)
 + "identified_no" = the reference number assigned to the name  
 + "difference" = if there is a taxonomic classification difference or note about the classifications
 + "accepted_name" = the accepted name for dubitable occurrences
 + "accepted_rank" = rank of above accepted taxonomic name
 + "accepted_no" = ref number assigned to accepted name
 + "early_interval" = the earliest epoch during which the occurrence is found
 + "late_interval" = the latest epoch during which the occurrence is found
 + "max_ma" = the oldest age in millions of years at which the occurrence is found
 + "min_ma" = the youngest age in millions of years at which the occurrence is found
 + "reference_no" = the ID number of publication in which the occurrence is referenced
 + "paleomodel" = the model upon which the paleogeography is based
 + "paleolng" = the paleolongitude coordinates at which the occ. is found
 + "paleolat" = the paleolatitude coordinates at which the occ. is found
 + "geoplate" = the geoplate number upon which the occ. was located
 + "phylum" = the phylum to which the occ. belongs
 + "class" = the class to which the occ. belongs
 + "order" = the order to which the occ. belongs
 + "family" = the family to which the occ. belongs
 + "genus" = the genus to which the occ. belongs

5)
> points(Anthozoa[,"paleolng"],Anthozoa[,"paleolat"])

6) Most of the Eastern Hemisphere Anthozoan occurrences occurr in the Mediterranean region. Because Anthozoans are marine organisms, this infers that this region featured a prevalent marine setting at the time.

Problem Set 3

1)
> Periss<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleocene",StopInterval="Oligocene")

2)
Perrisodactyls are odd-toed ungulates, typically large herbivores including rhinocerases, horses, tapirs and their ilk.

3)
> subset(Periss,Periss[,"collection_no"]==112723)

4)
The geoplate id associated with this collection is number 501. 

5)
This geoplate id corresponds to the Indian subcontinent.

6)
The region-X, also known as India, tectonically careens from the mid-Indian Ocean northnorth-eastward to collide with the Asian continent and foment the Himalayan orogenic event.

7)
It is unlikely that Perissodactyla migrated from region-X to China during the Paleogene, because when both are plotted on a Paleogene paleomap, the two plates do not yet make contact. This means that the organisms represented by occurrences of Perissodactyla on region-X (which acts as an isolated province for most of the Paleogene) must have arrived to the plate before it was separated from the rest of the continents in Pangea, but the fact that Perissodactyls already exist on China before region-X makes landfall shows that they could not have arrived to China by rafting over on region-X. Rather, the map shows that Perissodactyls had spread throughout the North American, African, Eurasian and Indian continents by the Paleogene, which supports the hypothesis that the China and Indian occurrences had arrived independently to those plates from a third region where the taxon first developed and originated, back during Pangea, allowing for the dispersal of the taxon before continental breakup. 
