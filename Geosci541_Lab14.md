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

Several of these taxa, particularly the first four, are poor data likely because they have such short names that there can be many unrelated taxa using those letters as prefixes, creating a biased number of incidences of these short names occurring near the letters "pyr."

Conversely, the large taxa names are unlikely to have been accidentally a part of unrelated names, and are much more likely to actually represent taxa that are commonly pyritized. Additionally, invertebrates are much more commonly found in pyritized fossil form, so the arthropods and particularly marine invertebrates are likely to represent good data (marine organisms deposited deep in the oceans and in redox conditions are far more susceptible to reducing environments which produce pyritized fossils).

#### Problem Set 2

````R
> my_counts<-count_uses(my_taxa[,"taxon_name"],0,pyr)
> my_counts <- my_counts[order(-my_counts[,"matches"]),]
> my_counts
       string matches
53       foram     143
47       trace      91
1        plant      85
3         wood      55
45       ammon      54
36     ammonit      46
22    ostracod      42
13        mite      40
61   microfoss      33
55      bivalv      29
31   gastropod      22
59   gastropod      22
57       spong      21
24        lice      20
54       phyco      18
28     mollusc      15
10    trilobit      14
46    trilobit      14
39  brachiopod      13
17      insect      11
48      echino      11
67        horn      11
7    arthropod      10
30        fish       9
58   nannofoss       7
62     vertebr       7
68     crinoid       7
6         worm       6
8        coral       6
32  cephalopod       6
34      oyster       6
37      nautil       6
50       coral       6
44     echinod       5
56     baculit       5
29        clam       4
38      bryozo       4
16     crustac       3
4        flora       2
33       squid       2
52        leaf       2
63        bird       2
12      spider       1
15        crab       1
21      shrimp       1
27     annelid       1
40      beetle       1
51     annelid       1
65      mammal       1
2         moss       0
5      nematod       0
9     anthozoa       0
11    arachnid       0
14    scorpion       0
18    myriapod       0
19   centipede       0
20   millipede       0
23     hexapod       0
25     arnacle       0
26 lophotrocho       0
35     scallop       0
41         bug       0
42    dragonfl       0
43      cnidar       0
49     porifer       0
60       snail       0
64     reptile       0
66       shark       0
69    starfish       0
````

Using a mixture of informal and partial formal names, we see a much broader pattern of data occurrences. Formans/foraminifera top the list, followed by trace fossils. Plants and wood follow, showing the clear benefit of more general and informal search terms. Ammon has more occurrences than ammonit, showing an inclusion of the more general ammonoid mentions.

I aimed to choose as many diverse names for different invertebrate and marine phyla and orders in the vernacular, and as often as possible kept group names shorter to include a range of suffixes, while not being so short as to include unrelated clades (case in point, "ammonit" or "ammon" to include all mentions of ammonites, ammonitic fossil units, ammonoids, etc.).

Both the truncated formal names and our list of informal names include arthropods high up: ostracods and crustaceans, and insects. However, our list eliminates the top four erroneous short names from the formal list, and includes broader and less formal groups such as forams. While I would more likely trust our informal list because it includes far more data occurrences, it still might be subject to some poor results: for example, while trace fossils are sometimes pyritized, having 91 occurrences through out NPL system suggests some taxa occurring near "pyr" begin with the phrase "trace-."
