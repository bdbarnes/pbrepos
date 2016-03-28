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
 + "identified_name"
 [7] "identified_rank"
 "identified_no"  
 [9] "difference"
 "accepted_name"  
[11] "accepted_rank"
"accepted_no"    
[13] "early_interval"
"late_interval"  
[15] "max_ma"          
"min_ma"         
[17] "reference_no"    
"paleomodel"     
[19] "paleolng"        
"paleolat"       
[21] "geoplate"        
"phylum"         
[23] "class"           
"order"          
[25] "family"          
"genus" 
