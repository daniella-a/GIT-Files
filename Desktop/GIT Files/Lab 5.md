Daniella Assing
Geosci 541
Feb 28 2016
Lab #5

> 11/20 Points :(
> Come see me next time you have problems.

## Problem Set 1
You may not use vegan( ) for this subsection.

1) What is Bivalve generic richness in the Miocene? What code did you use to find out?

Richness - total number of unique species. 

````R
#Find the dimensions of the matrix
> dim(BivalveAbundance)
[1]   29 2272
> sum(BivalveAbundance[20, 1:2272] > 0)
[1] 634
````

2) What is the Berger-Parker Index of Brachiopods genera in the Pliocene? What code did you use to find out? [Hint: the function max( ) may help you).

````R
> max(BrachiopodAbundance[27, 1:3107])
[1] 22
> which((BrachiopodAbundance[27, ]) == 22)
Terebratula 
        446 
> sum(BrachiopodAbundance[27, 1:3107] > 0)
[1] 23
> 22/23
[1] 0.9565217 
````

> -1 Points

3) What is the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
> 1-sum(((BrachiopodAbundance[5, 1:3107])/3107)^2)
[1] 0.9154911
````

4) What is the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?

````R
> LateCretSum<-sum(BivalveAbundance["Late Cretaceous", ])
> LateCretAbundance<-BivalveAbundance["Late Cretaceous", ]
> NewAbundance<-LateCretAbundance[LateCretAbundance>0]
> A <-NewAbundance/LateCretSum
> B <-log(NewAbundance/LateCretSum)
> C <-sum(A*B)
> -1*C
[1] 5.086512
````

5) What is the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

````R
> PaleoceneSum<-sum(BivalveAbundance["Paleocene", ])
> PaleoceneAbundance<-BivalveAbundance["Paleocene", ]
> NewPaleoceneAbundance<-PaleoceneAbundance[PaleoceneAbundance>0]
> A<-NewPaleoceneAbundance/PaleoceneSum
> B<-log(NewPaleoceneAbundance/PaleoceneSum)
> C<-sum(A*B)
> -1*C
[1] 4.511063
````

6) What is the percent change in Shannon's Entropy between the Late Cretaceous and the Paleocene? Can you think of any major events that happened between the Late Cretaceous and Paleocene that might be relevant to biodiversity? [Hint: Use google if you don't know.] Is this reflected in this index?

````R
> (Paleocene-LateCret)/LateCret*100
[1] -11.31426
Yes, the end-Cretaceous mass extinction is a major event altered biodiversity. This is reflected in the index since it is a negative number which shows that biodiversity decreased.
````

7) What if you use the exp( ) function to exponentiate the Shannon's Entropies you calculated in questions 4,5, and 6 (i.e.,e^Shannon's Entropy)? What percent of diversity is gained/lost? Does this better reflect the change between the Late Cretaceous and Paleocene? Why or why not?

````R
> ExpPaleocene<-exp(Paleocene)
> ExpLateCret<-exp(LateCret)
> (ExpPaleocene-ExpLateCret)/ExpLateCret*100
[1] -43.75764
````

It might better reflect the change as an exponential function is also projected and may gave a larger range so it may be more accurate.

## Problem Set 2
Install (if you have not already) and load the vegan package into R. Read the help file for the diversity( ) function - ?diversity or help(diversity). You must have already loaded the vegan package in order for it to run.

1) Use the specnumber( ) function (also from the vegan package) to find Bivalve richness in the Miocene. What code did you use to find out?
> specnumber(BivalveAbundance["Miocene", ], , MARGIN = 1)
[1] 634

2) Use the diversity( ) function to find the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?
> diversity(BrachiopodAbundance["Late Ordovician", ], index = "shannon", MARGIN = 1, base = exp(1))
[1] 4.664635

3) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?
> diversity(BivalveAbundance["Late Cretaceous", ], index = "shannon", MARGIN = 1, base = exp(1))
[1] 5.086512

4) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?
> diversity(BivalveAbundance["Paleocene", ], index = "shannon", MARGIN = 1, base = exp(1))
[1] 4.511063

## Problem Set 3

1) Is brachiopod richness positively, negatively, or un-correlated with bivalve richness? Show your code?

````R
> OutOrder<-array(c(3.755572,3.227148,3.560792,3.148909,3.628257,3.567614,3.294253,3.844638, 3.988784, 3.397504, 3.149485, 4.259922, 4.571792, 4.922718, 5.086512, 4.894056, 4.410415, 3.357938, 4.511063, 5.375537, 4.972140, 4.299667, 5.267982, 4.454766, 4.127591, 4.516975, 5.334865, 4.160419, 2.905877),dimnames=list(c("Pennsylvanian", "Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli", "Mississippian", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Early Ordovician", "Paleocene", "Miocene", "Oligocene", "Early Jurassic", "Pleistocene", "Guadalupian", "Middle Triassic",  "Late Triassic", "Pliocene", "Lopingian", "Early Triassic")))

#My code after the one above wouldn’t work!

> InOrder<-OutOrder[c("Middle Ordovician”,"Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian","Middle Devonian","Late Devonian","Mississippian","Pennsylvanian","Cisuralian", "Guadalupian","Lopingian","Early Triassic","Middle Triassic","Late Triassic","Early Jurassic","Middle Jurassic","Late Jurassic","Early Cretaceous","Late Cretaceous","Paleocene","Eocene","Oligocene","Miocene","Pliocene","Pleistocene")]
Error: unexpected symbol in "InOrder<-OutOrder[c("Middle Ordovician”,"Late"
````

> I think it is because you confused a curly " with a straight "
> - 1 Points

2) Is brachiopod biodiversity positively, negatively, or un-correlated with bivalve biodiversity when using the Gini-Simpson index? Show your code?

> -1 Points

3) Looking just at changes in brachiopod richness through time, when did the greatest drop in brachiopod richness occur (i.e., between what two consecutive epochs)?

> -1 Points

## Problem Set 4
1) Repeat the above steps, but for the BrachiopodAbundance community matrix. What is the standardized richness you got for brachiopods. Show your code.

````R
> SampleAbundances<-apply(BrachiopodAbundance,1,sum)
> SampleAbundances[which(SampleAbundances==min(SampleAbundances))]
Pleistocene 
         63 
> StandardizedRichness<-apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> StandardizedRichness[1:6]
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician 
            42.63             34.42             38.70             46.71             41.11 
       Llandovery 
            41.72 
````

2) How does the standardized brachiopod richness (previous question) compare to the unstandardized brachiopod richness from Problem Set 3? Show your code. Explain your reasoning. [Hint: Don't forget to put your biodiversities in temporal order]

> -1 Points

3) Make a scatter plot of standardized brachiopod richness versus standardized bivalve richness. Make a second scatter plot of unstandardized brachiopod richness versus unstandardized bivalve richness. Compare and contrast the two plots. What are the differences or similarities? Does standardizing or not standardizing matter? Show your code and explain your reasoning in detail. [Hint: If you forgot how to plot, revist the previous lab]

> -2 Points

4) Do you believe that there is any evidence in these analyses to support the idea that bivalves outcompeted brachiopods over time? Explain your reasoning.

````R
Pennsylvanian Middle Ordovician   Late Ordovician        Llandovery 
         3.755572          3.227148          3.560792          3.148909 
          Wenlock            Ludlow           Pridoli     Mississippian 
         3.628257          3.567614          3.294253          3.844638 
   Early Devonian   Middle Devonian     Late Devonian        Cisuralian 
         3.988784          3.397504          3.149485          4.259922 
    Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous 
         4.571792          4.922718          5.086512          4.894056 
  Middle Jurassic  Early Ordovician         Paleocene           Miocene 
         4.410415          3.357938          4.511063          5.374768 
        Oligocene    Early Jurassic       Pleistocene       Guadalupian 
         4.972140          4.299667          5.267982          4.454766 
  Middle Triassic     Late Triassic          Pliocene         Lopingian 
         4.127591          4.516975          5.334865          4.160419 
   Early Triassic 
         2.905877 

TemporalOrder<-array(c(3.227148,  3.560792 ,  3.148909 , 3.628257, 3.567614, 3.294253, 3.988784, 3.397504, 3.149485, 3.844638, 3.755572, 4.259922, 4.454766, 4.160419, 2.905877,  4.127591, 4.516975, 4.299667, 4.410415, 4.571792, 4.894056, 5.086512, 4.511063, 4.922718, 4.972140, 5.374768, 5.334865, 5.267982),dimnames=list(c(“Middle Ordovician”, “Late Ordovician”, “Llandovery”, “Wenlock”, “Ludlow”, “Pridoli”, “Early Devonian”, “Middle Devonian”, “Late Devonian”, “Mississippian”, “Pennsylvanian”, “Cisuralian”, “Guadalupian”, “Lopingian”, “Early Triassic”, “Middle Triassic”, “Late Triassic”, “Early Jurassic”, “Middle Jurassic”, “Late Jurassic”, “Early Cretaceous”, “Late Cretaceous”, “Paleocene”, “Eocene”, “Oligocene”, “Miocene”, “Pliocene”, “Pleistocene”)))
````

> -2 Points
