# 1964-Racial-Riots
This project was inspired by this lesson on the Programming Historian (https://programminghistorian.org/en/lessons/finding-places-world-historical-gazetteer#65-named-entity-recognition).

## Process

### Step 1: Sourcing

I used NewspaperSg to find contemporary newspapers from the Straits Times (https://eresources.nlb.gov.sg/newspapers/). I looked through newspapers published around the dates of the riots until I stopped seeing reports of riots to ascertain the range of dates to focus on. I then read through those newspapers and took screenshots of passages where locations were mentioned. To reduce workload, not all articles were used (The selection was arbitrary).

The articles used are as follows:

22 July 1964: APPEAL FOR CALM (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640722-1.2.2)

23 July 1964: UNDER CONTROL: Razak (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640723-1.2.3)

5 September 1964: STOP PRESS (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640905-1.2.6)

6 September 1964: Situation improves in S’pore (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640906-1.2.6)

7 September 1964: Two-hour break in curfew this afternoon (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640907-1.2.3)

8 September 1964: Curfew cut again in S’pore (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640908-1.2.3)

9 September 1964: Another death only major incident in S’pore (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640909-1.2.66)

10 September 1964: Day curfew lifted in S’pore (https://eresources.nlb.gov.sg/newspapers/digitised/article/straitstimes19640910-1.2.114)

### Step 2: Processing

Having acquired the necessary texts, I used PyTesseract’s optical character recognition function to digitise them, followed by spaCy to perform named entity recognition to identify the locations mentioned (For a more detailed explanation, please refer to newspaper_extraction.ipynb).

The results of this analysis showed that a majority of violent incidents occurred in Geylang, the City Area, and Tanjong Pagar.

The locations and their corresponding texts were compiled into an Excel spreadsheet.

### Step 3: Creating the Maps

Using the 1963 map provided by OneMap (https://www.onemap.gov.sg/historicalmaps/#), I downloaded map tiles corresponding to the above areas and combined them together using PowerPoint. This resulted in three maps: the Geylang, City and Tanjong Pagar maps. This meant that some incidents were not mapped as they fell outside of the mapped areas.

### Step 4: Plotting the Incidents

Using QGIS, I georeferenced the three maps onto a modern map of Singapore. I then plotted the location of the violent incidents onto two point layers (based on month) and joined the Excel spreadsheet to the layers (I recognise that it would be more efficient to input the text directly onto the layers, but I wanted to practice my joining skills).

Afterwards, I created GIFs showing the progression of violent incidents across time. 

### Step 5: Making the Webmap

Following that, I created a webmap to allow users to interact with the map. I used the QGIS2WEB plugin to export a Leaflet map. Leaflet was chosen over OpenLayers due to its ease of modification, which was necessary for the following steps.

I then created a slider to control the opacity of the historical maps for easier juxtaposition of violent incidents against modern locations (Google AI search was used to generate part of the code for the slider given my inexperience with JavaScript). 

I noticed that not all points were rendered as their descriptions were longer than 255 characters (https://github.com/qgis2web/qgis2web/issues/947). Thus, I re-exported the points layers to SHP files and regenerated the webmap using them. I then edited the data and index files to ensure the descriptions were correct.

## Reflections

### Historical

For a more accurate list of violent incidents, a wider range of sources should have been used. However, due to time, language and other practical constraints, I decided to rely on the Straits Times as my sole source. 

Practical constraints meant that I did not have much time to sift through the many articles and thus, I performed only a cursory search through the newspapers selected, further affecting the accuracy of my list.

This project focused more on data visualisation rather than any historical analysis. An interesting angle to pursue would be to analyse the possible correlation between the location of violent incidents and racial makeup (e.g.,  what was Geylang’s racial makeup such that it saw the brunt of violent incidents?) A possible source to carry out such analysis would be to use the 1957 Census as it lists the racial breakdown of various areas (https://www.nlb.gov.sg/main/book-detail?cmsuuid=7b306d60-16c1-458d-a9ef-6be4cb6b1821). I had considered pursuing such analysis, but decided against it as I would have to manually georeference the various areas, which would have been time-consuming. 

### Technology

A possible way to improve on data collection would be to write a programme that would access the URLs of the various articles and take screenshots of them automatically. This would have saved time and effort. In doing so, it would also improve the accuracy of data collection as it would ensure that all incidents were captured, given that it removes the need for me to manually comb through the newspapers and articles, which necessitates arbitrary selection to reduce workload (For more reflections on the data collection process, please refer to newspaper_extraction.ipynb).

Instead of using PowerPoint to join the various map tiles together, another programme could have been used instead, as the exported images from PowerPoint were of low quality as compared to the original map tiles from OneMap (or maybe I’m just bad at PowerPoint).

A slider could have been added to the webmap to allow users to control the time and see the progression of the riots, similar to the GIFs. Unfortunately, my JavaScript skills were insufficient for the task (It took me three days to figure out how to add a slider and make it work).
