Daniella Assing
Geosci 541
Feb 15 2016
Lab #3

> Great Job! 18.8/20

1)	How many collections are associated with this references?
704 collections are associated with this reference.

2)	What is the reference id number for the article?
The reference ID number is 24429.

1)	The first taxon in the taxonomic list is Rafinesquina alternata. Next to the taxonomic name is the citation (Conrad 1830), what is the significance of this citation?
This is done for two reasons: (1) to give credit to the person(s) who first classified this taxon and (2) to provide evidence that this is peer-reviewed work that has been accepted in the scientific community.

2)	What is the class, order, family, genus, and species name of the second taxon in the taxonomic list?
Strophomenata - Strophomenida - Strophomenidae - Strophomena planumbona 

3)	In what County was the data collected?

It was collected in Union county, Indiana. 

4)	What age (Period) is the data from?

The data is from the Ordovician.

5)	What is the geologic formation where the data was found?

The data was found in the Liberty Formation.

1)	Zoom in so that you can see from Texas to Florida and from Florida to New York. You can zoom using the mouse wheel, by double-clicking, or clicking the + and - signs. Some of the occurrences are orange and others are yellow, what is the significance of the different colors?

The different colours show the ages of the sample. For example the yellow circles are Cenozoic and the orange are Paleogene.

2)	Zoom back out. Add an additional filter into the search bar, the Ypresian stage. The Ypresian is a time interval ranging from 47.8–56.0 million years ago. In what countries are there Ypresian occurrences of Abra?

There are Ypresian occurrences of Abra in England and Belgium.

3)	Clear the Abra and Ypresian filters from the search. Look for the genus Ambonychia. Within the United States find the city with the most occurrences of Ambonychia. What is the name of this city?

Cincinnati.

4)	What age (Period) are most Ambonychia occurrences?

Late Ordovician.

Add in your answer to question 4 as an additional filter. Click on the little icon of South America breaking away from Africa on the left side of the screen. This icon rotates the continents back to their position in the specified time-period. Note that it requires you to have set a specific time-period as a filter.
1)	During this time-period, were most occurrences of Ambonychia arrayed parallel or perpendicular to the equator?

I think that most occurrences are arrayed parallel to the equator.

2)	Click on the little insect icon on the left side of the screen. This brings up taxonomic information on the target taxon. What order does Ambonychia belong to?

Ambonychia belongs to the order Myalinida. 

## Exercise Questions 3

For the following questions generate the appropriate URL for the following data queries.

1)	What is the appropriate URL for downloading all occurrences of Ambonychia in the Lexington Limestone as a JSON?
https://training.paleobiodb.org/data1.2/colls/list.json?datainfo&rowcount&base_name=Ambonychia&strat=Lexington Limestone

2)	What is the appropriate URL for downloading all occurrences of mammals present in the Paleocene through Oligocene epochs as a csv?
https://training.paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name=mammal&interval=paleocene,oligocene

3)	What is the appropriate URL for downloading all opinions on the order Testudines in the Mesozoic?
https://training.paleobiodb.org/data1.2/taxa/opinions.csv?datainfo&rowcount&base_name=Testudines&rank=order&interval=Mesozoic,Mesozoic

4)	What is the appropriate URL for downloading all collections of Aves, Marsupialia, and Sirenia in the United States as a csv?
https://training.paleobiodb.org/data1.2/colls/list.csv?datainfo&rowcount&base_name=Aves, Marsupialia, Sirenia&cc=US

5)	What is the appropriate URL for downloading all occurrences of the gastropod genus Ficus as a csv?
https://training.paleobiodb.org/data1.2/colls/list.csv?datainfo&rowcount&base_name=ficus&taxon_reso=genus

> Close, but you need Gastropoda:Ficus to ensure you get Ficus the snail not the plant

## Exercise Questions 4

The next set of questions is free form, in that you can find the answer to the following questions using any of the PBDB tools discussed so far.

1)	What family does the genus Gastrocopta belong to?

It belongs to the family Gastrocoptidae.

2)	There is only one occurrence of Isoetes in Portugal. What age is it?

It is Aptian in age.

3)	What is the age of the oldest occurrence of Gastrocopta?

The age of the oldest occurrence of Gastrocopta is Late Miocene, although I did find a specimen that says “subgenus” and “obsolete variant of” that is Rupelian. 

> I'm not sure where you got this? The oldest occurrence is Bridgerian in the Eocene. -1 points

4)	There is only one occurrence of Tiktaalik in the Paleobiology Database? Was that occurrence located in the tropics or the extratropics when it was alive?

It was located in the tropics when it was alive.

5)	There are two occurrences of Namacalathus in Siberia. What geologic formations are they found in?

(a)	the Kotodzha Formation
(b)	the Raiga Formation

## Exercise Questions 5
https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Pliocene

1)	In Lab Exercise 2 you downloaded a csv file of ammonite sizes from a github URL directly into R.What code would you use to download the above PBDB data directly into R?

URL<-"https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Pliocene"
PlioceneMammals<-read.csv(URL,row.names=1)
PlioceneMammals

2)	Download the above data into R. What are its dimensions?

class(PlioceneMammals)
[1] "data.frame"

dim(PlioceneMammals)
[1] 39 12

The dimensions are 39 rows and 12 columns. 

3)	Did the above call use the occurrences, collections, references, opinions, or specimens route?

It called the collections.

4)	What genus is being called for? What is its colloquial name? What age did I limit the data query too?

The genus Mammut is being called for. The colloquial name is “mastodon”. The age of the data is limited to the Pliocene.

5)	Look through the service documentation for the appropriate route (based on your answer to Question 2). Find out how to extend the age search to range from the Miocene Epoch through to the Pleistocene Epoch. Give the new data query URL.

URL<-"https://paleobiodb.org/data1.2/occs/list.csv?base_name=Mammut&interval=Miocene,Pleistocene"

6)	I want the data query to show me the paleocoordinates (i.e., paleolatitude and paleolongitude) of each data point. Give the updated data query URL.

URL<-"https://paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name=Mammut&interval=Miocene,Pleistocene&show=paleoloc”

## Question 6

1)	Write an R function that will take a taxonomic name (as a character string) and an interval (as a character string) as its argument, and will download all fossil occurrences into R. See above.

Morphologic Measurements
Some species have morphologic data attached to them in the Paleobiology Database. Let's consider the following three species of Ammonite: Glyptophiceras sinuatum, Xenoceltites variocostatus, and Submeekoceras mushbachanum.
Each of these species have morphologic data (e.g., shell width measurements) attached to them in the paleobiology database. You can search for this information by searching taxonomic names here.

1)	Each of the ammonite specimens in Part I of Lab 2 belongs to one of these three species. Based on 1) the morphologic information on these three species in the Paleobiology Database and 2) the morphologic information from Lab 2, can you tell which specimens belong to which species? Explain your reasoning.
I encounter the same problem here as I did in Lab 2 because of the possibility of sexual dimorphism and the effects of ontogeny in the organisms. I calculated the mean w:d ratio for each species using the values given in the database but I found that in many cases this was not a good way to differentiate the species. I also tried classifying them based on the minimum and maximum values but also taking into consideration the various types of ribbing. I found that this was a slightly better way to classify them, especially differentiate between Species A and B since, although they appear similar in size their ribbing is different. However I don’t think that shell width, height and diameter along with the ribbing are good ways to tell the species apart because (1) juvenile specimens may have no ribs but also be of a species that eventually develops them and they could be confused with the juvenile/adult species with no ribs (Species C of Lab 2) (2) the changes in shell diameter/height/width may be because of sexual dimorphism with females being larger than males, and without knowing the difference between the juvenile and the adult, a small juvenile could be mistaken for an adult male.

> Good Answer

2)	Look up Xenoceltites variocostatus in the Paleobiology Database. Find the first person (journal paper/reference) to name this species. (Hint: Both the first and second author's last names start with "B"). What is the name of the article?
Brayard and H. Bucher. 2008. Smithian (Early Triassic) ammonoid faunas from northwestern Guanxi (South China): taxonomy and biochronology, Fossils and Strata, 55:1-179.

3)	Do a google scholar search for this article. Open it and scroll down to the "Plates" subsection. You should see various pictures of different ammonites towards the very end of the article. Find the pictures of Xenoceltites variocostatus. Based on the features in these pictures, can you identify which specimens in Part I of Lab 2 belong to this species?
I would say that most of the species I listed for Species B in Lab 2 belong to this species. After having seen more samples in the book, I re-categorised some species into this group.

Lab 2 answer:
Group 2 - Species B
-ribs visible on shell but are very close together
-average u:d ratio may be in-between
Samples 25, 22, 15, 12, 10, 9, 4 
Final answer: 25, 24, 22, 21, 15, 13, 12, 10, 9, 4, 2
