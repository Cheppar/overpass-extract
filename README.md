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
{ "type": "Feature", "properties": { "full_id": "r146656", "osm_id": "146656", "osm_type": "relation", "admin_level": "8", "boundary": "administrative", "name": "Manchester", "name:el": "Μάντσεστερ", "name:ur": "مانچسٹر", "type": "boundary", "wikidata": "Q21525592", "wikipedia": "", "ISO3166-2": "GB-MAN", "council_name": "Manchester City Council", "council_style": "city", "designation": "metropolitan_district", "name:ar": "مانشستر", "name:cy": "Manceinion", "name:he": "מנצ'סטר", "name:ko": "맨체스터", "ons_code": "00BN", "ref:gss": "E08000003", "source:ons_code": "OS_OpenData_CodePoint Codelist.txt" }, "geometry": { "type": "MultiPolygon", "coordinates": [ [ [ [ -2.27362, 53.42248 ], [ -2.27372, 53.42254 ], [ -2.27404, 53.42269 ], [ -2.27458, 53.42291 ], [ -2.27525, 53.42317 ], 

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











