Daniella Assing
Geosci 541
Lab 9 
March 28 2016

> 19.5/20

1) Is North America currently (i.e., in the present) to the West or East of its position in the Cretaceous?

North America is currently west of its position compared to the Cretaceous.

2) Look at the following line of code that you used before.

````R
plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)
Describe what this code is doing. A good answer will describe what each of the plot( ) function arguments is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does the rgb( ) function do? What does it mean? Use google or the R help( ) function.
col= is responsible for the colour of the overall image.
lty= controls the opacity of the map.
rgb() allows you to pick a specific colour. 
add=TRUE adds previous data on top of each other, for example, it will overlay several maps.
````

> - 0.5 Points, lty= controls the style of lines used. Opacity is determined by rgb( ).

3) Download a map of the middle Cretaceous (Albian Epochs ~110 mys ago). Name it AlbianMap.
````R
> AlbianMap<-downloadPaleogeography(Age=110)
````

4) Add AlbianMap to the plot you made earlier. The added continents should be colored green, and use the same level of opacity (translucence) as your CretaceousMap and ModernMap. Show your code!
````R
> plot(AlbianMap,col=rgb(0,1,1,0.33),lty=0,add=TRUE)
````

5) Has there been more movement north and south or east and west in the Eastern Hemisphere since the Albian?

There has been more movement north and south (but more north) in the Eastern Hemisphere since the Albian.

6) Has there been more movement north and south or east and west in the Western hemisphere since the Albian?

There has been more east-west movement in the Western Hemisphere since the Albian (mostly westward).

## Problem Set 2

1) Download and plot a new map of the Paleocene/Eocene boundary (Use google to find the age of this boundary, remember the `downloadMap( )` function only takes whole numbers). You may use any color and level of opacity. Show your code.
````R
> PalEoBoundaryMap<-downloadPaleogeography(Age=55)
> plot(PalEoBoundaryMap,col=rgb(0,1,0,0.33),lty=0)
````

2) Download a dataset of Anthozoa occurrences from the paleobiology database ranging from the Paleocene through Eocene. Consult with previous labs if you do not remember how to do this. Show your code.

<strike> > library("paleobioDB", lib.loc="~/R/win-library/3.2")</strike>

````R
> DataPBDB<-downloadPBDB(Taxa=c("Anthozoa"),StartInterval="Paleocene",StopInterval="Eocene")
> DataPBDB<-cleanRank(DataPBDB)
> Epochs<-downloadTime(Timescale="international epochs")
> DataPBDB<-constrainAges(DataPBDB,Epochs)
````

3) How many occurences did you download?

````R
> dim(DataPBDB)
[1] 2694   26
````

4) What are the names of columns of the PBDB data matrix you just downloaded. What does each column mean? If you do not know, consult with the API documentation.

````R
> dimnames(DataPBDB)[[2]]
 [1] "occurrence_no"
A positive integer that uniquely identifies the occurrence.
   "Record_type"
The type of this object: occ for an occurrence.
    "reid_no"  
If this occurrence was reidentified, a unique identifier for the reidentification.      
 [4] "flags" 
This field will be empty for most records. A record representing an identification that has been superceded by a more recent identification will have the letter R in this field.
"collection_no"   
The identifier of the collection with which this occurrence is associated.
"Identified_name"
The taxonomic name by which this occurrence was identified.
 [7] "identified_rank"
The taxonomic rank of the identified name, if this can be determined.
"Identified_no"
The unique identifier of the identified taxonomic name.
"Difference"
If the identified name is different from the accepted name, this field gives the reason why. This field will be present if, for example, the identified name is a junior synonym or nomen dubium, or if the species has been recombined, or if the identification is misspelled.

[10] "accepted_name"
The value of this field will be the accepted taxonomic name corresponding to the identified name.
  "Accepted_rank"
The taxonomic rank of the accepted name. 
  "Accepted_no"
The unique identifier of the accepted taxonomic name in this database.    
[13] "early_interval"
The specific geologic time range associated with this occurrence (not necessarily a standard interval), or the interval that begins the range if late_interval is also given.
 "Late_interval"
The interval that ends the specific geologic time range associated with this occurrence, if different from the value of early_interval.
 "Max_ma"
The early bound of the geologic time range associated with this occurrence (in Ma).       
[16] "min_ma"
The late bound of the geologic time range associated with this occurrence (in Ma)
"Reference_no"
 The identifier of the reference from which this data was entered   
"Paleomodel"
The primary model specified by the parameter pgm.
[19] "paleolng"
The paleolongitude of the collection, evaluated according to the primary model indicated by the parameter pgm.
"paleolat"        
The paleolatitude of the collection, evaluated according to the primary model indicated by the parameter pgm.
"Geoplate"
The identifier of the geological plate on which the collection lies, evaluated according to the primary model indicated by the parameter pgm. This might be either a number or a string.       
[22] "phylum"
The phylum corresponding to each occurrence.
"class"           
The taxonomic classification of the occurence: phylum, class, order, family, genus.
"order"          
The order corresponding to each occurrence.
[25] "family"          
The family corresponding to each occurrence.
"genus"   
The genus corresponding to each occurrence, if the occurrence has been identified to the genus level. This block is redundant if class or classext are used.       
````

5) Use the points( ) function to plot each occurrence on the map you made previously (make sure to use the paleolatitude and paleolongitude coordinates). Show your code. If you do not know how to use the points( ) function, consult the help file or use Google.

````R
> plot(PalEoBoundaryMap,col=rgb(0,1,0,0.33),lty=0.01)
> points(DataPBDB[ ,"paleolng"],DataPBDB[ ,"paleolat"])
````

6) Where are most of the Anthozoa occurrences in the Eastern Hemisphere (i.e., what region of the world)? Are Anthozoans primarily marine or freshwater organisms? What can you infer must have existed in this region of the world during this time?
Most of them occur in Europe and Turkey. They are primarily marine organisms. A shallow marine shelf environment must have existed at this time, but I’m a little confused because this is not what’s shown on the map.

> An epicontinental ocean!

## Problem Set 3

1) Download a dataset of Perissodactyla occurrences from the PBDB that span the Paleogene. Show your code.

````R
> DataPBDB2<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleocene",StopInterval="Oligocene")
> DataPBDB2<-cleanRank(DataPBDB2)
> Epochs<-downloadTime(Timescale="international epochs")
> DataPBDB2<-constrainAges(DataPBDB2,Epochs)
````

2) What is the defining attribute of Perissodactyla? What are some prominent examples (e.g., lions, tigers, bears, oh my!)? [Hint: Neither lions, nor tigers, nor bears are members of Perissodactyla.]
Horses, rhinos and tapirs are some prominent examples. Their middle toe is largest and defines the plane of symmetry of the foot.

3) Find collection number 112723 in the dataset you just downloaded in Question 1. Show your code.

````R
> DataPBDB2<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleocene",StopInterval="Oligocene")
> which(DataPBDB2[,"collection_no"]==112723)
[1] 3949 3951
> DataPBDB2[3949, ]
     occurrence_no record_type reid_no flags collection_no          identified_name identified_rank identified_no
3949        961980         occ      NA    NA        112723 Eotitanops pakistanensis         species        169823
     difference            accepted_name accepted_rank accepted_no early_interval late_interval max_ma min_ma
3949            Eotitanops pakistanensis       species      169823       Ypresian                   56   47.8
     reference_no paleomodel paleolng paleolat geoplate   phylum    class          order          family      genus
3949        36699     gp_mid     70.7     2.76      501 Chordata Mammalia Perissodactyla Brontotheriidae Eotitanops
> DataPBDB2[3951, ]
     occurrence_no record_type reid_no flags collection_no      identified_name identified_rank identified_no difference
3951        963172         occ      NA    NA        112723 Balochititanops haqi         species        192106           
            accepted_name accepted_rank accepted_no early_interval late_interval max_ma min_ma reference_no paleomodel
3951 Balochititanops haqi       species      192106       Ypresian                   56   47.8        36699     gp_mid
     paleolng paleolat geoplate   phylum    class          order          family           genus
3951     70.7     2.76      501 Chordata Mammalia Perissodactyla Brontotheriidae Balochititanops
````

4) What "geoplate" id (tectonic plate) is associated with this collection? What modern day region of the world does this geoplate id correspond to? The remaining questions will refer to this geoplate/region as region-X.

The geoplate id associated with this collection is 501. The modern-day region that this plate corresponds to is Pakistan.

5) Subset your dataset of Perissodactyla occurrences to only include occurrences that occur in region-X. How many occurrences are there? Show your code.

````R
> PeriData<-subset(DataPBDB2,DataPBDB2[,"geoplate"] == 501)
> nrow(PeriData)
[1] 75
````

6) Using the maps we have created previously, making your own new maps, or using the Paleobiology Database Navigator tool, what is the general history of region-X from the Albian through to the present day?
Using the Paleobiology Database Navigator tool; Region X has been identified as Pakistan.

I see two parts that could be Pakistan. I looked up which tectonic plate it belongs to and it appears that half of it belongs to the Eurasian plate and half to the Indian plate. For this answer I’ll assume that all of Pakistan is on the Indian plate. In the Albian the Indian plate is completely detached and as time progresses it moves northward to join the Eurasian plate. Pakistan becomes for the most part land-locked with only one opening to the sea (south Pakistan).

7) There are also many Paleogene occurrences of Perissodactyla in present day China. Using the maps we have created previously, making your own new maps, or using the Paleobiology Navigator tool, evaluate the plausibility of each of the following scenarios? Thoroughly explain your reasoning and how you tested your ideas.

●	Species of Perissodactyla migrated from region-X to China during the Paleogene?
This species probably did not migrate from region X to China. In the Paleocene the Indian plate is completely surrounded by water, but there are early occurrences of this species in North America. The only way for this species to get to China during this time period is by travelling by land through North America to Eurasia. 

●	Species of Perissodactyla migrated from China to region-X during the Paleogene?
I think this also occurred but at first glance at the map during the Eocene it is a little hard to imagine how land animals would cross bodies of water to get to Pakistan. However I think that the inland water at this period could have been a shallow interior sea or there could have been shallow rivers that dried periodically on timescales too small to be captured by the Paleobiology Database Navigator, so these dry areas don’t show up. In this way, this species could have crossed from China to India during the Eocene.

●	The species of Perissodactyla in China and region-X are unrelated and probably both came from a third region?
This appears to be the case because the earliest occurrence of this species in the Paleocene is in North America which becomes attached to Eurasia, so it is more probable that the species migrated to China and the Pakistan which both have younger occurrences.

