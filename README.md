# chattanooga-od-sample

The geographic area under consideration is the Hamilton county, Tennessee. The county is further divided into census tracts(larger, poor resolution) and census block groups (CBGs) (smaller, better resolution). We find the movement matrix of people travelling for jobs(LODES) or other putposes (Safegraph)

## The data

1. Geographic data

The geographic data of Hamilton county defines the area and boundaries of the census tracts and CBGs. It also provides unique GEOIDs for each zone under consideration, which we can further use to find relevant regions in other datasets. It is in .shp format.

2. People movement<br>
  a. [LODES dataset]()<br> 
  b. Safegraph dataset

These provide the information about the movement of people (the number of people moving, and their origin and destination CBG). 

3. Residential and Commercial locations

The locations of residential and commercial areas are obtained from OpenStreetMaps(OSM). They are obtained by using the [OSM Accomodation tags](https://wiki.openstreetmap.org/wiki/Key:building#Accommodation) and the python library OSMNX. 

4. Microsoft Buildings dataset (complements to OSM locations)

These are the locations of all buildings in Hamilton county, obtained from [Microsoft Building Footprints](https://github.com/Microsoft/USBuildingFootprints), and are **not labelled** as home/commercial places. These locations are used in lieu of OSM labelled locations only in case the concerned CBG has no home/commercial locations from OSM. 



