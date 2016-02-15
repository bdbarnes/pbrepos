Geosci 541 Ð Paleobiology
Lab Exercise 2 (2/8/16)
Ben Barnes

## Part 1

1) I qualitatively identified three main morphotypes which I hypothesized three species for:

+ Thick sigmoidal ribbed with ceratitic suture Ð 1, 2, 6, 8, 11, 12, 13, 18, 20, 21
+ Thin biconcave ribbed Ð 4, 9, 10, 16, 22, 24
+ Smooth ribs with apparent siphuncle line Ð 3, 5, 7, 14, 15, 17, 19, 23, 25

Not every specimen exhibited all of the listed features, but each was grouped with as similar as possible fossils.

````R
> Ammonitelist <- list(Species1,Species2,Species3)
> Ammonitelist
[[1]]
   Specimen Diam Umb:Diam Wdth:Diam Strat                       Species
1         1 61.0     0.45      0.23   8.1 Thick sigmoid ribbed ceratite
2         2 20.0     0.33      0.26   8.9 Thick sigmoid ribbed ceratite
6         6 11.5     0.41      0.35   8.7 Thick sigmoid ribbed ceratite
8         8 68.5     0.48      0.22  10.3 Thick sigmoid ribbed ceratite
11       11 73.5     0.47      0.26   9.6 Thick sigmoid ribbed ceratite
12       12 20.9     0.41      0.29   4.9 Thick sigmoid ribbed ceratite
13       13 43.5     0.40      0.20   3.4 Thick sigmoid ribbed ceratite
18       18 11.8     0.38      0.34   4.0 Thick sigmoid ribbed ceratite
20       20 44.5     0.38      0.23  10.7 Thick sigmoid ribbed ceratite
21       21 40.5     0.41      0.22   9.5 Thick sigmoid ribbed ceratite

[[2]]
   Specimen Diam Umb:Diam Wdth:Diam Strat             Species
4         4 39.5     0.34      0.23   8.5 Thin biconcave ribs
9         9 56.0     0.39      0.23   9.1 Thin biconcave ribs
10       10 50.0     0.35      0.23   8.1 Thin biconcave ribs
16       16 45.5     0.28      0.23   1.3 Thin biconcave ribs
22       22 48.0     0.35      0.23   4.2 Thin biconcave ribs
24       24 20.0     0.40      0.28   5.1 Thin biconcave ribs

[[3]]
   Specimen Diam Umb:Diam Wdth:Diam Strat       Species
3         3 35.0     0.39      0.23   3.7 Smooth suture
5         5 28.0     0.29      0.29   3.1 Smooth suture
7         7 33.0     0.42      0.22   7.2 Smooth suture
14       14 16.0     0.26      0.32   3.2 Smooth suture
15       15 35.5     0.39      0.23   4.7 Smooth suture
17       17 31.0     0.32      0.23   8.3 Smooth suture
19       19 63.5     0.29      0.23   4.7 Smooth suture
23       23 23.0     0.33      0.28   3.0 Smooth suture
25       25 59.5     0.34      0.21   6.8 Smooth suture
````


2) Each species was identified primarily through qualitative means, rather than quantitative. Species1 was identified by the presence of thick ribs roughly exhibiting a sigmoidal shape; in the case of juveniles and smaller samples, it was more difficult to establish the thickness of the ribs. However, the deciding factor was typically a knobby appearance in profile due to the thick ribs.     Species2 was identified by the close grouping of thin biconcave growth lines/ribs, particularly closer to the aperture. Specimens in profile were typically smooth, an often slightly asymmetrical around the aperture. Species 3 was identified by the presence of a siphuncle line along the coiled body, and relatively smooth ribbing or sutures. Often this species exhibited tighter coiling towards the center. Although species assignment was made based on qualitative observations, quantitative comparisons shows important distinctions between the three groups. Outliers in each group could be attributed to interspecies variation, dimorphism, or damaged specimens leading to incorrect species identification.

````R	
mean(Species1[,ÓDiamÓ] = 39.57
mean(Species2[,ÓDiamÓ] = 43.17
mean(Species3[,ÓDiamÓ] = 36.06
	
# However, due to dimorphism and ontogenetic changes, diameter may be a useless comparison.

mean(Species1[,ÓUmb:DiamÓ] = 0.412
mean(Species2[,ÓUmb:DiamÓ] = 0.3517
mean(Species3[,ÓUmb:DiamÓ] = 0.3367

mean(Species1[,ÓWdth:DiamÓ] = 0.2600
mean(Species2[,ÓWdth:DiamÓ] = 0.2383
mean(Species3[,ÓWdth:DiamÓ] = 0.2489
````

The difference in means can be statistically tested using the expert concepts function:

````R
compareammonites <- function(Species1,Species2,Iterations=100){
	Barrel <- c(Species1[,"Umb:Diam"],Species2[,"Umb:Diam"])
	ReplicatedMeans <- array(data=NA,dim=Iterations)
	for(Counter in 1:Iterations){
		NewSpecies1 <- sample(Barrel,dim(Species1)[[1]],replace=TRUE)
		NewSpecies2 <- sample(Barrel,dim(Species2)[[1]],replace=TRUE)
		Species1Mean <- mean(NewSpecies1)
		Species2Mean <- mean(NewSpecies2)
		ReplicatedMeans[Counter] <- Species1Mean-Species2Mean
		}
	return(ReplicatedMeans)	
	}
ReplicationResults <- compareammonites(Species1,Species2,100)
Length(which(ReplicationResults>=0.0603))
[1] 2

# Meaning that approximately 2/100 trials would yield a difference of this magnitude, or p=0.02.
````

For the other species comparisons:

````R
compareammonites(Species2,Species3,100) for ÒUmb:DiamÓ (for which results >=0.015)
	p = 0.30 (NOT statistically significant)
compareammonites(Species1,Species3,100) for ÒUmb:DiamÓ (for which results >=0.0753)
	p = 0.00 (statistically significant)
````

Now for ÒWdth:DiamÓ:
compareammonites(Species1,Species2,100) for ÒWdth:DiamÓ (for which results >=0.0217)
	p = 0.17 (NOT statistically significant)
compareammonites(Species3,Species2,100) for ÒWdth:DiamÓ (for which results >=0.0106)
	p = 0.27 (NOT statistically significant)
compareammonites(Species1,Species3,100) for ÒWdth:DiamÓ (for which results >=0.0111)
	p = 0.36 (NOT statistically significant)

From these statistical tests it is clear that we cannot support the hypothesis that there is significant difference among species groups for the Wdth:Diam dimension, and not for all groups of Umb:Diam. This shows that it is possible 1) species do not significantly vary in these dimensions, 2) grouping together multiple ontogenetic stages and sexes confounds possible significant differences among species, or 3) we have incorrectly grouped species groups that would otherwise be significantly different. 

3) I infer that the juvenile specimens can be qualitatively identified in each species by size in respect to number of growth lines/ribs/coils (smaller/less developed in juveniles). This is also apparent by a significant size difference.
	
+ Juvenile Species1: 2, 6, 12, 18
+ Juvenile Species2: 24
+ Juvenile Species3: 5, 14, 23

As ontogenetic development in each species occurs, ribs and sutures develop more prominently, size increases greatly, and the number of coils increases. The juvenile image in profile is often less symmetrical than their well-developed counterparts.

4) Each Species group in the list was converted to AdultSpecies by removing the above juvenile specimen data. Following this, histograms were plotted to show the distribution of diameter, U:D, and W:D dimensions among adult specimens Ð the hypothesis being that if sexual dimorphism exists in each species, the female specimens will be appreciatively larger than the male. Particularly in AdultSpecies 1 and 3 the histograms for diameter and U:D showed bimodality, suggesting the existence of sexual dimorphism. In AdultSpecies2, there is either less-pronounced dimorphism, no dimorphism, or the sample of 5 specimens is too small to show a trend. Some of the graphs are shown below.

## Part 2

1) The plethodon list is composed of the elements: Òland,Ó Òlinks,Ó Òspecies,Ó Òsite,Ó and Òoutline.Ó
	(Used name(plethodon))

2) Respectively: array, matrix, factor, factor, and matrix. (Used class(plethodon[[1]], etc.)

3) Using dim(plethodon[[1]]), dim= 12 (rows), 2 (columns), 40

#### Subsection 2

1) Based on the two columns for x- and y-coordinate information, hummingbird[[1]] ÒlandÓ records the landmark data.

2) 
````R
> ProcrustesHummingbirds <- gpagen(hummingbirds[["land"]])
````

3) 
````R
> plotTangentSpace(ProcrustesHummingbirds[["coords"]],warpgrids=FALSE,verbose=FALSE)
````

4) There is no clear clustering of specimen data, and so there is no significant evidence that there is more than one hummingbird species.

## Part 3

1) The synapomorphy, or shared derived trait, for species D and E is fangs > 6 inches.

2) A plesiomorphy (shared ancestral trait) of the clade containing species D and E is a sulfurous odor.

3) A synapomorphy for species A and B is adorable eyelashes.

4) The sulfurous odor is present in taxa C, D, and E.

5) Species D is distinguished from species E for a lack of derived laser death ray trait.

6) Adorable eyelashes are present in more than one taxon, and are thus a synapomorphy.

7)	
+ Family 1: monophyletic (contains MRCA and all descendants)
+ Family 2: <strike>paraphyletic</stirke> (contains MRCA but not all descendants i.e. A, D, and E) polyphyletic
+ Family 3: monophyletic (contains MRCA and all descendants)

8) This is inadvisable, due to the fact that D and E share two derived traits that A does not, and A features two derived traits that D and E do not, whereas there are no shared derived traits between A, and D and E.

9)	
+ Group 1: paraphyletic (contains MRCA but not all descendants i.e. D and E)
+ Group 2: monophyletic (contains MRCA and all descendants)
+ Group 3: paraphyletic (contains MRCA but not all descendants i.e. E)
+ Group 4: monophyletic (contains MRCA and all descendants
+ Group 5: polyphyletic (contains recent descendants without MRCA)

Part 4
1. The most likely type of heterochrony responsible for the evolution of these two species is paedomorphosis: the ancestral Gryphaea arcuata exhibits a round shell shape in juvenile stage but develops into a much narrower shell as it ages, as its shell simultaneously thickens. Conversely, the more derived adult descendants show rounder shell shapes and thinner shells, showing an expression of traits which were formerly juvenile characteristics.

2. Graphaea gigantea has undergone a greater degree of paedomorphosis heterochrony, as evidenced by its closer resemblance to the juvenile of the ancestral Gryphaea arcuata (a much rounder and thinner shell).

3. Olenellus in this figure undergoes paedomorphosis as well, where the small size and horned carapace of the juvenile ancestral is progressively expressed in the descendants. Additionally, the shallow depth and increased T¼/oxygen content which marked the environment in which the ancestral juvenile lived is reflected in the progressive niche evolution of the descendants, taking on not just the morphological but the environmental characteristics of O. lapworthi juveniles.

