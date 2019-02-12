# Querying the C3S311a Lot 2 WFS

## Overview of Web Feature Service

The C3S311a Lot2 project provides a Web Feature Service (WFS) implemented in GeoServer. 

This provides a web service API as the interface layer to the harmonised land and marine database held on JASMIN. The database is deployed in Postgres with PostGIS geospatial extensions.

## Availability of the WFS

The WFS is currently publicly accessible via the endpoint:

 http://glamod1.ceda.ac.uk/geoserver/glamod/ows?service=WFS&version=1.0.0&request=GetCapabilities

The above URL provides an XML document describing the capabilities of the service.

## Detailed WFS Interface

The service interface enables complex filtering of the following tables/views, exposed as "feature types" within the WFS specification:

- `source_configuration_web`
- `station_configuration_web`
- `header_table_web`
- `observations_table_web`
- `report_table_web`

Details of the filter rules are provided at:

 https://docs.geoserver.org/latest/en/user/filter/
 
However, this is a complex interface that provides a broad range of queries. We propose the use of the simple query interface described below as a starting point.

## Simple Query Interface

The simple query interface provides access to the table "view" known as: `report_table_web`
