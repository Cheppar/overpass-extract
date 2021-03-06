# overpass-extract

The purpose of this document is to provide a clear understanding of extracting city boundaries from OpenStreetMap (OSM) using OSM_ID.

## STEP 1: Overpass with QGIS
- We will use OverPass API in QGIS
This makes it easy for anyone with minimal knowledge of writing code and more precise as compared to using the Overpass browser API. 

To understand why, please feel free to visit the URL ``` https://overpass-turbo.eu/ ```

In QGIS ensure you have installed the plugins'

``` 
Plugins --> Manage and Install Plugins
```  
A pop-up window will appear and search for : ``` Quick OSM ```

Quick OSM Plugin contains the ```overpass API```

Launch the ``` QUICK OSM ``` plugin follow this path.

``` Vector -> QuickOSM -> QuickOSM ```.

--------------------------------------------
## Step 1.2 :  Overpass with JS. 
This example uses OpenStreetMap data, fetched from the OverpassAPI.        
65606 is the OSM ID for the relation of the greater London boundary used in this
example, it can be viewed online here:
        
``` http://www.openstreetmap.org/relation/1370729```
        
                

```  var query = '(relation(65606);>>->.rels;>;);out;';

        $.get("//overpass-api.de/api/interpreter?data=" + query, function(data) {

            var geoJSON = osmtogeojson(data, {
                polygonFeatures: {
                    buildingpart: true
                }
            });
```

The code is simple, ensure your query has the correct OSM_ID
From the table of OSM_ID provided, feel free to replace the city OSM_ID boundary to display data.
Currently, thinking of searching more than one OSM_ID per search request.

------
## Step 2 :  Extracting Boundaries. 

``` Key ``` : ``` boundary ```

``` value ``` : ``` administrative ```

``` in ```

It's important to copy the ```OSM_ID``` from the list of cities. 
for London use  ```OSM_ID``` : ```65606```

``` A village or Town ``` : ``` OSM_ID ```

click on the Run Query button. 
The boundary will be extracted displaying relevant boundaries, points and any relevant features.

The importance of using the overpass API, it generates a query for you to apply in the ```https://overpass-turbo.eu/ ``` 

After extraction, export data as GeoJSON. 

The GEOJSON format can be used universally, it meets the relevant format 

```
{
"type": "FeatureCollection",
"name": "manchestercity",
"crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:OGC:1.3:CRS84" } },
"features": [
{ "type": "Feature", "properties": { "full_id": "r146656", "osm_id": "146656", "osm_type": "relation", "admin_level": "8", "boundary": "administrative", "name": "Manchester", "name:el": "????????????????????", "name:ur": "??????????????", "type": "boundary", "wikidata": "Q21525592", "wikipedia": "", "ISO3166-2": "GB-MAN", "council_name": "Manchester City Council", "council_style": "city", "designation": "metropolitan_district", "name:ar": "??????????????", "name:cy": "Manceinion", "name:he": "??????'??????", "name:ko": "????????????", "ons_code": "00BN", "ref:gss": "E08000003", "source:ons_code": "OS_OpenData_CodePoint Codelist.txt" }, "geometry": { "type": "MultiPolygon", "coordinates": [ [ [ [ -2.27362, 53.42248 ], [ -2.27372, 53.42254 ], [ -2.27404, 53.42269 ], [ -2.27458, 53.42291 ], [ -2.27525, 53.42317 ], 

```

The sample query is can be accessed from the query pane in the left tab. 

The above query is displayed as 
```
[out:xml] [timeout:25];
 {{geocodeArea:303685}} -> .area_0;
(
    node["boundary"="administrative"](area.area_0);
    way["boundary"="administrative"](area.area_0);
    relation["boundary"="administrative"](area.area_0);
);
(._;>;);
out body;

```

This code can be run on the overpass website and extract boundaries and export in geojson format.

## STEP 3: Extracting OSM_ID

We use a simple URL to query the data

``` https://nominatim.openstreetmap.org/search?format=json&city=london&country=uk ```

Use case of greater London city boundary. 

``` &city = london ```

``` &country = uk ```

Returned Data 

``` 
[{"place_id":332008866,"licence":"Data ?? OpenStreetMap contributors, ODbL 1.0. https://osm.org/copyright","osm_type":"relation","osm_id":65606,"boundingbox":["51.2867601","51.6918741","-0.5103751","0.3340155"],"lat":"51.5073219","lon":"-0.1276474","display_name":"London, Greater London, England, United Kingdom","class":"boundary","type":"administrative","importance":0.9307827616237295,"icon":"https://nominatim.openstreetmap.org/ui/mapicons//poi_boundary_administrative.p.20.png"},{"place_id":283161129,"licence":"Data ?? OpenStreetMap contributors, ODbL 1.0. https://osm.org/copyright","osm_type":"relation","osm_id":51800,"boundingbox":["51.5068696","51.5233122","-0.1138211","-0.0727493"],"lat":"51.5156177","lon":"-0.0919983","display_name":"City of London, Greater London, England, United Kingdom","class":"boundary","type":"administrative","importance":0.6865111547516773,"icon":"https://nominatim.openstreetmap.org/ui/mapicons//poi_boundary_administrative.p.20.png"}]
```

## STEP 3: Using an Open source Scraper

The tool is a simple chrome extension with capabilities of extracting datasets from HTML elements with classes.

```` https://webscraper.io/ ````

I advise interested individuals to view online tutorials for a rigorous guide on how to use it.

### Steps
 1. Create a sitemap. Name it London , and copy this URL 

``` https://nominatim.openstreetmap.org/ui/details.html?osmtype=R&osmid=65606 ```

2. Add selectors. Selectors are the HTML tags with classes/id that contain relevant information. Choose your selectors. Click Add Selector -> 
   Selecting HTML tags. 
   Each selector must have an ID, Type = Text, Click on selector and hover over your desired HTML Element.
   The data will be highlighted, click on it to select.
   Ensure to save selector
   Please preview the data to confirm your results before launching the scraper.
   
3. Launching the scrapper
- Click on your sitemap. Usually name `sitemap xxxx` xxx represent the name of your scraper.
- A drop down will appear, select `Scrape`.
- Reduce the request interval to `1000 / 2000`. Simply the interval per scrape request. The interval must be above 1s. We must comply to OSM nominatim request.
- Refresh the scraper as indicated in the result pane to view your data.
- Export data as `.CSV` or `.XLSX` format.
- To continue extracting data replace the city name and country per request.

#### Findings

- This process is automated though repetitive as we have to constantly create various sitemaps to a specitic URL.
- We download several `XLSX` or `CSV` files that we later have to compile them.
- The easiest way would be the JSON data nominatim API.
- We still have to find the OSM_ID through method 1.
- The steps below are beneficial if we have the OSM_ID.














