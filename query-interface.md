# Querying the C3S311a Lot 2 WFS

## Overview of Web Feature Service

The C3S311a Lot2 project provides a Web Feature Service (WFS) implemented in GeoServer. 

This provides a web service API as the interface layer to the harmonised land and marine database held on JASMIN. The database is deployed in Postgres with PostGIS geospatial extensions.

## Availability of the WFS

The WFS is currently publicly accessible via the endpoint:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetCapabilities

The above URL provides an XML document describing the capabilities of the service.

## Detailed WFS Interface

The service interface enables complex filtering of the following tables/views, exposed as "feature types" within the WFS specification:

 - `source_configuration_web`
 - `station_configuration_web`
 - `header_table_web`
 - `observations_table_web`
 - `report_table_web`

This is a complex interface that provides a broad range of queries. We propose the use of the simple query interface described below as a starting point.

## Simple Query Interface

The simple query interface provides access to the table "view" known as: `report_table_web`

This view combines the two database tables in the Common Data Model:

 - Header Table: providing common header information relating to a set of observations.
 - Observations Table: the actual measurement values that make up the observation.
 
The `report_table_web` can be queried via a number of query parameters provided in the query string of an HTTP GET request. The query parameters are included in the `cql_filter` parameter of the query string.

The basic form of the query is:

```
http://glamod1.ceda.ac.uk/geoserver/glamod/ows?
    service=WFS&
	version=2.0.0&
	request=GetFeature&
	typename=report_table_web&
	outputFormat=json&
	cql_filter=<QUERY>
```

The value of `<QUERY>`, representing the filters, is specified using an extended version of the Common Query Language (ECQL). Documentation for ECQL can be found at:

 http://docs.geoserver.org/latest/en/user/filter/index.html

We focus on some specific options here:

 1. Station ID: `primary_station_id`
 2. Station Name: `station_name`
 3. Observed Variable: `observed_variable`
 4. Bounding Box: 
  - Using `BBOX` on `report_location`
 5. Time Window:
  - Using: `BEFORE`, `AFTER` on `report_timestamp`
 6. Station Type: `station_type`
  
Details of how these input arguments are specified are given in the examples below.
  
## Example queries

The following queries show how queries can be constructed for the options listed above. All queries should be appended on to the base URL:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=

### 1. Station ID: primary_station_id

To filter on the Station Identifier, you can include an exact term in the query:

 `primary_station_id=%27IC301881%27`

This will return all reports where the station ID contains the string "IC30188". 

A full list of station IDs can be found at:

 * TODO!

### 2. Station Name: station_name

If a station name, or partial name, is known then a query can be constructed to filter on it:

 `station_name%20ILIKE%20'%25kosmos%25'`
 
The function `ILIKE` is case insensitive. The example above extracts all reports where the station ID contains the string 'kosmos' irrespective of case.

A full list of station names can be found at:

 * TODO!

### 3. Observed Variable: observed_variable

Many users would like to filter on observed variable:

 `observed_variable=85`
 
The codes used for the observed variables can be found at:

 * https://github.com/glamod/common_data_model/blob/master/tables/observed_variable.dat
 * TODO! Provide a query to list observed variables directly from DB.

### 4. Bounding Box: BBOX on report_location

The location of an observation is recorded in the `report_location` geometry. This can be queried using the `BBOX` function:

 `BBOX(report_location,-20,-80,50,-50)`
 
This query filters for results in the region bounded by 20W to 50E and 80S to 50S. The format is therefore:

 `BBOX(report_location,<westernmost_longitude>,<southernmost_latitude>,<easternmost_longitude>,<northernmost_latitude>)`

### 5. Time Window: BEFORE, AFTER on report_timestamp

Temporal filtering can be performed using the predicates `BEFORE` and/or `AFTER` on `report_timestamp` field:

- Before  1933-12-31T23:59:59: 
  `report_timestamp%20BEFORE%201933-12-31T23:59:59Z`
- After   1933-01-01T00:00:00: 
  `report_timestamp%20AFTER%201933-01-01T00:00:00Z`
- Between 1933-01-01T00:00:00 and 1933-12-31T23:59:59:
  `report_timestamp%20AFTER%201933-01-01T00:00:00Z%20AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z`

### 6. Station Type: station_type

Results can be filtered by Station Type using the `station_type` field:

 `station_type=2`
 
This restricts the query to marine data (code=2) only.
 
The `station_type` codes are available from:

 * https://github.com/glamod/common_data_model/blob/master/tables/station_type.dat
 * TODO! Provide a query to list station types directly from DB.

## Combining filters for more complex queries

The Common Query Language (ECQL) allows multiple conditions to be provided as part of a single query by concatenating them together with "%20AND%20", for example:

- Station ID and Time constraint (BEFORE):

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z

- Station ID and Time constraint (AFTER):

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20AFTER%201933-01-01T00:00:00Z

- Station ID and Time window (BEFORE and AFTER):

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20AFTER%201933-01-01T00:00:00Z%20AND%20report_timestamp%20BEFORE%201933-11-30T00:30:00Z

- Station type, Observed Variable and Bounding Box:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=station_type=2%20AND%20observed_variable=85%20AND%20BBOX(report_location,-20,-80,50,-50)


## Responses

### Response types

The GeoServer WFS can provide the following responses:

 - ASCII comma separated values: `csv`
 - Keyhole Markup Language: `kml`
 - JavaScript Object Notation: `application/json`
 - Geography Markup Language (XML): `gml3`
 - Shapefile: `shape-zip`
 
### Modifying the Response fields

The GeoServer implementation of WFS allows the response fields to optionally be selected in the request.

The `propertyName` request parameter can be specified with a comma-separated list of values:

 https://docs.geoserver.org/stable/en/user/services/wfs/reference.html#getfeature
 
#### Example 1: Basic fields

The following example selects only some fields from the output:

 * date_time
 * observation_duration
 * observation_duration
 * observation_longitude
 * observation_latitude
 * observed_variable
 * observation_value
 * value_significance
 * units
 * date_time_meaning
 
As JSON:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=json&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z%20AND%20observed_variable=85&propertyName=date_time,observation_duration,observation_duration,observation_longitude,observation_latitude,observed_variable,observation_value,value_significance,units,date_time_meaning

As CSV: 

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=csv&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z%20AND%20observed_variable=85&propertyName=date_time,observation_duration,observation_duration,observation_longitude,observation_latitude,observed_variable,observation_value,value_significance,units,date_time_meaning
 
#### Example 2: Basic fields - sorted by Date Time

Here is the same query, with the added `sortBy=date_time` option in order to sort by that field:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=csv&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z%20AND%20observed_variable=85&propertyName=date_time,observation_duration,observation_duration,observation_longitude,observation_latitude,observed_variable,observation_value,value_significance,units,date_time_meaning&sortBy=date_time
 
And to reverse sort by Date Time (add `+D` (descending) to the `sortBy` parameter):

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=2.0.0&request=GetFeature&typename=report_table_web&outputFormat=csv&cql_filter=primary_station_id=%27IC301881%27AND%20report_timestamp%20BEFORE%201933-12-31T23:59:59Z%20AND%20observed_variable=85&propertyName=date_time,observation_duration,observation_duration,observation_longitude,observation_latitude,observed_variable,observation_value,value_significance,units,date_time_meaning&sortBy=date_time+D
