Daniella Assing
Geosci 541
April 11 2016
Lab 11
Problem Set 1

> 18.5/20

1) You first mission is to download a list of all Triassic units in the Macrostrat Database using the /units route into R. Name this object TriassicUnits. As always, show your code.

````R
>source("https://raw.githubusercontent.com/aazaff/paleobiologyDatabase.R/master/communityMatrix.R")
>URL<-"https://macrostrat.org/api/units?interval_name=Triassic&format=csv"
>TriassicUnits<-read.csv(URL,row.names=1)
````

2) How many Triassic units did you download? What code did you use to find out?

````R
> dim(TriassicUnits)
[1] 838  16
````

3) Look at the first 10 units that you downloaded. Are they mostly Igenous, Metamorphic, or Sedimentary rocks? Do you believe that these units are relevant for an investigation of fossil preservation? Show your code and explain your reasoning.

````R
> dimnames(TriassicUnits)[[2]]
 [1] "section_id"       "col_id"           "project_id"      
 [4] "col_area"         "unit_name"        "strat_name_id"   
 [7] "Mbr"              "Fm"               "Gp"              
[10] "SGp"              "t_age"            "b_age"           
[13] "max_thick"        "min_thick"        "outcrop"         
[16] "pbdb_collections"
> TriassicUnits$unit_name
[1] Metamorphic Igneous Complex                                                                      
  [2] Sur Series                                                                                       
  [3] Southern California Batholith and Santiago Peak Volcanics and Bedford Canyon Fm                  
  [4] Southern California Batholith and Santiago Peak Volcanics and Bedford Canyon Fm                  
  [5] Southern California Batholith and Santiago Peak Volcanics and Bedford Canyon Fm                  
  [6] Southern California Batholith and Santiago Peak Volcanics and Bedford Canyon Fm                  
  [7] Bonsall Tonolite                                                                                 
  [8] Southern California Batholith and Santiago Peak Volcanics and Bedford Canyon Fm                  
  [9] Unnamed                                                                                          
 [10] Central Gneiss Complex     
# These are mostly igneous and metamorphosed units. They are not relevant for investigating fossil preservation because volcanic activity destroys the fossils.
````

4) Which columns of your TriassicUnits data.frame denote the starting age and ending age of each unit, respectively? 

b_age denotes the starting (bottom or oldest)  age and t_age is the ending (top or youngest) age.

5) Considering the bottom and top ages of the first 10 units, are these units constrained to only the Triassic or do some range through the Triassic?
Most of them occur within the Triassic (252-201 Ma) although they all have age ranges which extend above and or/below the Triassic period. All the units include rocks younger than Triassic (t_age<201 Ma) and a few units are older than Triassic (b_age>252 Ma).

````R
> head(TriassicUnits$t_age, n=10)
 [1]  67.037  74.975  92.875  92.875  92.875  92.875  93.900  95.550 100.500 103.625
> head(TriassicUnits$b_age, n=10)
 [1] 259.9000 396.8750 203.1000 203.1000 203.1000 203.1000 261.9667 203.1000 396.8750 249.1750
````

## Problem Set 2
1) Re-download TriassicUnits, however, this time restrict the data to only sedimentary rocks. Show your code.

````R
URL<-"https://macrostrat.org/api/units?interval_name=Triassic&lith_class=sedimentary&format=csv"
TriassicSedimentary<-read.csv(URL, row.names=1)
````

2) Restrict TriassicUnits to only units that with starting ages <= start of the Triassic and ending ages >= to the end of the Triassic. As always, show your code.

Are we restricting TriassicUnits or TriassicSedimentary?

RestrictTriassic<-TriassicSedimentary[which(TriassicSedimentary[ ,"t_age"] >= 201 & TriassicSedimentary[ ,"b_age"] <= 252), ]

3) Repeat the above processes (download and subset) for the following geologic periods. The Cretaceous, Jurassic, Triassic (you don't have to download it twice), Permian, Carboniferous, Devonian, Silurian, and Ordovician. Show your code, but do not show me the downloaded data.
Are we isolating the sedimentary rocks like above too? (that’s what I’ve done) 

````R
# Cretaceous:
>URLcret<-"https://macrostrat.org/api/units?interval_name=Cretaceous&lith_class=sedimentary&format=csv"
>CretaceousUnits<-read.csv(URLcret,row.names=1)
>RestrictCretaceous<-CretaceousUnits[which(CretaceousUnits[ ,"t_age"] >= 65 & CretaceousUnits[ ,"b_age"] <= 145), ]
Jurassic:
>URLjur<-"https://macrostrat.org/api/units?interval_name=Jurassic&lith_class=sedimentary&format=csv"
>JurassicUnits<-read.csv(URLjur,row.names=1)
>RestrictJurassic<-JurassicUnits[which(JurassicUnits[ ,"t_age"] >= 145 & JurassicUnits[ ,"b_age"] <= 199), ]
Triassic:
>URL<-"https://macrostrat.org/api/units?interval_name=Triassic&lith_class=sedimentary&format=csv"
>TriassicSedimentary<-read.csv(URL, row.names=1)
>RestrictTriassic<-TriassicSedimentary[which(TriassicSedimentary[ ,"t_age"] >= 201 & TriassicSedimentary[ ,"b_age"] <= 252), ] 
Permian:
>URLper<-"https://macrostrat.org/api/units?interval_name=Permian&lith_class=sedimentary&format=csv"
>PermianUnits<-read.csv(URLper,row.names=1)
>RestrictPermian<-PermianUnits[which(PermianUnits[ ,"t_age"] >= 252 & PermianUnits[ ,"b_age"] <= 299), ]
Carboniferous:
>URLcar<-"https://macrostrat.org/api/units?interval_name=Carboniferous&lith_class=sedimentary&format=csv"
>CarboniferousUnits<-read.csv(URLcar,row.names=1)
>RestrictCarboniferous<-CarboniferousUnits[which(CarboniferousUnits[ ,"t_age"] >= 299 & CarboniferousUnits[ ,"b_age"] <= 359), ]
Devonian:
>URLdev<-"https://macrostrat.org/api/units?interval_name=Devonian&lith_class=sedimentary&format=csv"
>DevonianUnits<-read.csv(URLdev,row.names=1)
>RestrictDevonian<-DevonianUnits[which(DevonianUnits[ ,"t_age"] >= 359 & DevonianUnits[,"b_age"] <= 419), ]
Silurian:
>URLsil<-"https://macrostrat.org/api/units?interval_name=Silurian&lith_class=sedimentary&format=csv"
>SilurianUnits<-read.csv(URLsil,row.names=1)
>RestrictSilurian<-SilurianUnits[which(SilurianUnits[ ,"t_age"] >= 416 & SilurianUnits[,"b_age"] <= 444), ]
Ordovician:
>URLord<-"https://macrostrat.org/api/units?interval_name=Ordovician&lith_class=sedimentary&format=csv"
>OrdovicianUnits<-read.csv(URLord,row.names=1)
>RestrictOrdovician<-OrdovicianUnits[which(OrdovicianUnits[ ,"t_age"] >= 444 & OrdovicianUnits[ ,"b_age"] <= 488), ]
4) Make a vector named UnitFreqs that records the number of units present in each epoch. Show your code.
>UnitFreqs<-c(nrow(RestrictCretaceous),nrow(RestrictJurassic),nrow(RestrictTriassic),nrow(RestrictPermian),nrow(RestrictCarboniferous),nrow(RestrictDevonian),nrow(RestrictSilurian),nrow(RestrictOrdovician))
>UnitFreqs
[1] 4600  879  527  903 2960 1909 1243 2103
````

5) Find the mean and standard deviation of UnitFreqs not counting the Triassic. How many standard deviations above or below the mean is the number of Triassic Units? Show your code.

````R
>FreqWithoutTriassic<-c(nrow(RestrictCretaceous),nrow(RestrictJurassic),nrow(RestrictPermian),nrow(RestrictCarboniferous),nrow(RestrictDevonian),nrow(RestrictSilurian),nrow(RestrictOrdovician))
>mean(FreqWithoutTriassic)
[1] 2085.286
>sd(FreqWithoutTriassic)
[1] 1334.333
> (2085.286-527)
[1] 1558.286
> 1558.286/1334.333
[1] 1.167839 (standard deviations below the mean)
````

6) Given your answer to the above, do you believe that the Triassic has a statistically lower number of units than the other periods? Why?

It is 1.16 SDs below the mean so this would imply that it does have a statistically lower number of units.

> why? -0.5 points

7) What if you consider both the Triassic and Jurassic as potential outliers? Explain (show your code) how you arrived at your answer.

````R
>FreqNoTriassicJurassic<-c(nrow(RestrictCretaceous),nrow(RestrictPermian),nrow(RestrictCarboniferous),nrow(RestrictDevonian),nrow(RestrictSilurian),nrow(RestrictOrdovician))
> mean(FreqNoTriassicJurassic)
[1] 2286.333
> sd(FreqNoTriassicJurassic)
[1] 1340.524
> 2286.333-(879+527)
[1] 880.333
> 880.333/1340.524
[1] 0.6567081
````

If they are both considered outliers, the SD is still below the mean. However, it is closer to the mean compared to the previous calculation where only the Triassic was treated as an outlier.

> This is incorrect -1 Points

## Problem Set 3

1) Download and plot a map of all North American geologic columns (no color). Show your code.

````R
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
>GotURL<-getURL(URL)
>NorthAmerica<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(NorthAmerica,col=)
```` 

2) On top of your map from Question 1, plot a map of all North American columns with Induan-Anisian sedimentary units. Use the Olenekian hexcode color for this map. You can look up the Olenekian hexcode through the /defs/intervals route.

````R
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=242&age_bottom=252&project_id=1"
>GotURL<-getURL(URL)
>Induan<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(Induan,col="#B051A5",add=TRUE)
````

3) Using the downloadPBDB( ) function from previous labs. Download all occurrences of animal fossils in the Paleobiology Database of Induan-Anisian age. Using the points( ) function, plot all of these occurrences on the map you made in question 2 as solid circles. If you do not remember how to use points, you can consult previous labs or use help(points). Show your code. Save this map for later questions.

````R
>Induan<-downloadPBDB(Taxa=c("Animalia"),StartInterval="Induan",StopInterval="Anisian")
>points(Induan[ ,"lng"],Induan[ ,"lat"],pch=20,col="lightgreen")
```` 
 
4) You can open a new plot window using quartz( ) if you are on a mac or `windows( ) if you are on a windows machine. Download and plot a map of all North American geologic columns (no color) - i.e., repeat Question 1 in this new plot window. On top of this map, plot a map of all North American columns with Lopingian aged sedimentary units. Use the appropriate Lopingian hexcode color for this new map. Show your code.

````R
#North America
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
>GotURL<-getURL(URL)
>NorthAmerica<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(NorthAmerica,col=)
#Lopingian Units
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=252&age_bottom=260&project_id=1"
>GotURL<-getURL(URL)
>Lopin<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(Lopin,col="#FBA794",add=TRUE)
 ````
 
5) Download all occurrences of animal fossils in the Paleobiology Database of Lopingian age. Plot all of these occurrences on the map you made in question 2 as solid circles. Show your code.

````R
#North America map with Lopingian units:
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=252&age_bottom=260&project_id=1"
>GotURL<-getURL(URL)
>Lopin<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(Lopin,col="#FBA794",add=TRUE)
#Downloading Lopingian fossils and plotting points:
>LopinFossils<-downloadPBDB(Taxa=c("Animalia"),StartInterval="Lopingian",StopInterval="Lopingian")
>points(LopinFossils[ ,"lng"],LopinFossils[ ,"lat"],pch=20,col="blue")
 ````
 
6) Compare and contrast your Induan-Anisian map versus your Lopingian map. Does it seem based on these maps that...

+	There was a substantial drop in the areal extent of North American sedimentary units across the P/T boundary.

Based on my maps (Permian in orange, Triassic in purple) it does seem that across the P/T there is a rise in sea-level (and hence, a drop in the aerial extent of North American sedimentary rocks) because there are just a few more sedimentary units recorded for the Permian than for the Triassic. A rise in sea-level would imply less aerial extent.

+	There was a substantial drop in the percentage of sedimentary units with reported fossils in them aross the P/T boundary?

There actually seems to be a substantial increase in the percentage of units reported with fossils. However this is not very surprising when we take into account that after mass extinctions taxa tend to radiate rapidly and to overshoot their recovery (I think I worded that weirdly. The taxa tend to recover to levels higher than pre-extinction).

●	Overall, do you think there is sufficient evidence from these maps to reject or accept the hypothesis that lower diversity in the Early Triassic is an artefact of either poor fossil sampling of the available sedimentary rock or a low availability of sedimentary rock.

The second hypothesis would definitely have to be rejected here because as we can see from the maps, there are slightly more sedimentary rocks in the Permian but yet this period has a much lower fossil data occurrence than the Triassic, which actually shows less sedimentary rock being preserved but tons more fossils.  Also, low diversity in the Triassic in comparison to what? If this is being compared to the Permian then I think from the maps we would instead expect an increase in diversity since there are more fossils being preserved even though there’s less sedimentary rock available. I don’t believe that we can learn about diversity here in any case though (unless it’s to make a very general assumption) because when I plotted these maps, only the occurrences were plotted (not individual species). 
It could very well be that the Permian is undersampled though, because from the maps I think that the extent of carbonate deposition is pretty well mirrored on both sides. 

 
