Cuyahoga County Plot
====================

Map of number and age of buildings in Cleveland by census tract. Future planes include employement, income, and foreclosure data.


# Converting ESRI shapefile to TopoJSON format

Make sure that ogr2 and TopoJSON are installed properly, see "Let's make a map!" (http://bost.ocks.org/mike/map/) for further instructions



 ``` tl_2013_39_tract.shp``` (via http://catalog.data.gov/dataset/tiger-line-shapefile-2013-state-ohio-current-census-tract-state-based)
 ``` cleveland_housing_age.csv ``` (for city of Cleveland, data taken by census tract from http://neocando.case.edu/cando/index.jsp?page=)
  
  
Take the census tract data for Cuyahoga County, ID 035

``` ogr2ogr -f GeoJSON -where "COUNTYFP = '035'" input35.json tl_2013_39_tract.shp ```

Add attributes to the GeoJSON file, mapping the id property from the shapefile (originally) to the column title in the csv file

```bash 
topojson \
-o output35.json \
-e cleveland_housing_age.csv \
--id-property=+NAME,+CensusTract \
-p since05=+Since05 \
-p 00to05=+00to05 \
-p 90to99=+90to99 \
-p 80to89=+80to89 \
-p 70to79=+70to79 \
-p 60to69=+60to69 \
-p 50to59=+50to59 \
-p 40to49=+40to49 \
-p pre40=+Pre40 \
--input35.json 
```
