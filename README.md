# chattanooga-od-sample

The geographic area under consideration is the Hamilton county, Tennessee. The county is further divided into census tracts(larger, poor resolution) and census block groups (CBGs) (smaller, better resolution). We find the movement matrix of people travelling for jobs (LODES), or general purposes (Safegraph).

## The data

1. Geographic data

The geographic data of Hamilton county defines the area and boundaries of the census tracts and CBGs. It also provides unique GEOIDs for each zone under consideration, which we can further use to find relevant regions in other datasets. It is initially in .shp format and has been stored in [ham_cbg.csv](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/data/ham_cbg.csv).

2. People movement<br>
  a. [LODES dataset](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/data/hamilton_lodes_2019.zip)<br> 
  b. Safegraph dataset

These provide the information about the movement of people (the number of people moving, and their origin and destination CBG). 

3. Residential and Work locations

    The locations of residential and commercial(work) areas are obtained from OpenStreetMaps(OSM). They are obtained by using the [OSM Accomodation tags](https://wiki.openstreetmap.org/wiki/Key:building#Accommodation) and the python library OSMNX. ([residential_locations.csv](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/data/ham_residential_buildings2.csv))
    
    The work locations are obtained as a combination of the tags [commercial](https://wiki.openstreetmap.org/wiki/Key:building#Commercial), [civic/amenity](https://wiki.openstreetmap.org/wiki/Key:building#Civic/amenity), and the Safegraph POI (point of interest) locations. ([work_locations.csv](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/data/work_loc_poi_com_civ.csv))

4. Microsoft Buildings dataset (complements to OSM locations)

These are the locations of all buildings in Hamilton county, obtained from [Microsoft Building Footprints](https://github.com/Microsoft/USBuildingFootprints), and are **not labelled** as home/work places. These locations are used in lieu of OSM labelled locations only in case the concerned CBG has no home/work locations from OSM. 
The data extraction is done as in [read_ms_buildings.ipynb](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/read_ms_buildings.ipynb).

## Deriving the OD matrix

We intend to find the Origin Destination (OD) matrix for Hamilton county. The home location acts as the **origin**, while the work location acts as the **destination**. It is obtained as a combination of the home location, work location, travel start time, and their return time. It is found by uniform sampling across the home and commercial locations.

There are a few assumptions made to help in the process of sampleing the data:
1. For the LODES and Safegraph data, we find the number of people travelling between each OD pair, and randomly sample the home and work locations from the OSM locations (or Microsoft Buildings if needed).
2. The travel start time(go_time) is sampled randomly from 7AM to 9AM (at 15min intervals)
3. The return time is sampled randomly from 4PM to 6PM (at 15min intervals)

For example if a OD pair has 50 people travelling among them, then we sample 50 home and 50 work locations and randomly choose 50 start and return times in the manner described.

The generated matrix is ...

The associated notebook - [movement_combinations.ipynb](https://github.com/smarttransit-ai/chattanooga-od-sample/blob/main/movement_combinations.ipynb)
