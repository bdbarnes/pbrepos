Geosci 541 Ð Paleobiology
Lab Exercise #6 (2/29/16)
Ben Davis Barnes
Problem Set 1

> 18/20

1)
> dim(DataPBDB)
[1] 34166    26
> dim(MacroPBDB)
[1] 9013   13
Total occurrences lost = 34166-9013 = 25153 occurrences

2) Macrostrat is a lithostratigraphic database which theoretically comprises all rock units and formations in the North American continent. However, the Paleobiology Database has data which extends worldwide therefore when matching them, the MacroPBDB list had to winnow out all of the non-North American occurrences.

 Problem Set 2
1)
> FrmOrderDiv <- specnumber(OrderMatrix)
> sort(FrmOrderDiv)

> CandidateUnits <- c("Chancellor","Kinzers Fm","Stephen Fm","Marjum Limestone","Wheeler Shale","Langston Fm","Weymouth Fm","Snowy Range Fm","Parker Slate","Forteau Fm")
> CandidateUnits <- as.vector(CandidateUnits)


2)
> GenusFrequencies <- colSums(GenusMatrix)

3)
> barplot(table(GenusFrequencies))

4)
Hollow Curve plot.

5)
> RareGenera <- subset(GenusFrequencies,GenusFrequencies<=2)

Problem Set 3
1)
> CandidateMatrix <- GenusMatrix[c(CandidateUnits),]

2)
> PercentShared
      Chancellor       Kinzers Fm       Stephen Fm 
       0.5714286        0.2586207        0.3055556 
Marjum Limestone    Wheeler Shale      Langston Fm 
       0.3559322        0.2307692        0.1632653 
     Weymouth Fm   Snowy Range Fm     Parker Slate 
       0.6764706        0.1951220        0.2812500 
      Forteau Fm 
       0.5652174
		Forteau Fm 
                                      14 
                            Parker Slate 
                                      16 
                          Snowy Range Fm 
                                      16 
                             Weymouth Fm 
                                      16 
                             Langston Fm 
                                      17 
                           Wheeler Shale 
                                      18 
                        Marjum Limestone 
                                      19 
                              Stephen Fm 
                                      23 
                              Kinzers Fm 
                                      24 
                              Chancellor 
                                      27
The mot likely candidates to be lagerstŠtten are the candidate units which have the greatest proportion of rare genera as well as having a high diversity of taxa, being the Chancellor (0.571 rare and 27 genera), the Weymouth Formation (0.676 rare and 16 genera), the Forteau Formation (0.565 rare and 14 genera), and the Stephen Formation (0.306 rare and 23 genera).

3) The Stephen Formation is famous for containing the Burgess Shale, the lagerstŠtten which contains some of the best-preserved soft-body fossils from the middle Cambrian and has revolutionized our understanding of early animal phyla, being the primary source of the earliest animal fossils until the discovery of the Chengjiang fauna in the Chinese Chiungchussu formation.

> The Chancellor group was the best candidate. It also contains the Burgess shale -2 points
