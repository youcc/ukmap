Make a UK map on Ubuntu using D3 and TopoJSON by following [Mike Bostock's example](https://bost.ocks.org/mike/map/).

### Downloaing geometry data
[Admin 0 - Details - map subunits](http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_map_subunits.zip)
[Populated Places](http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_populated_places.zip)

Upzip both files.

### Installing tools
```sh
$ sudo apt update 
$ sudo apt upgrade 
$ sudo apt-get install nodejs
$ sudo apt-get install npm
$ sudo apt install gdal-bin python-gdal python3-gdal
$ sudo npm install -g topojson
$ sudo ln -s /usr/bin/nodejs /usr/bin/node # 
```
### Converting data
```sh
$ ogr2ogr \
  -f GeoJSON \
  -where "ADM0_A3 IN ('GBR', 'IRL')" \
  subunits.json \
  ne_10m_admin_0_map_subunits.shp
  
$ ogr2ogr \
  -f GeoJSON \
  -where "ISO_A2 = 'GB' AND SCALERANK < 8" \
  place.json \
  ne_10m_populated_places.shp
  
$ topojson \
  -o uk.json \
  --id-property SU_A3 \
  --properties name=NAME \
  -- \
  subunits.json \
  place.json
```  
###- Loading data
  see index.html for details
  
### Run index.html in your local server to see the map 
