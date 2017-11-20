# Example queries to the GeoServer service

## Introduction

This page provides a number of example queries that can be made to the 
GeoServer service that sits in front of the Postgres database implementating 
the Common Data Model (CDM).

**Notes about the examples:**
 - The host is excluded in the examples below - you will need to add the correct hostname in order for the queries to work.
 - The URLs have been split into multiple lines to make them easier to view - you will need to convert them to a single line.
 
## Queries

### 1. Get contents of Observations Table in GML

http://<HOSTNAME>/geoserver/dyb/ows?service=WFS&version=1.0.0&
 request=GetFeature&
 typeName=dyb:observations_table_gis

### 2. Get a subset of the Observations table in KML

http://<HOSTNAME>/geoserver/dyb/ows?service=WFS&version=1.0.0&
 request=GetFeature&
 typeName=dyb:observations_table_gis&
 outputFormat=kml&
 cql_filter=
   BBOX(location, -20, -80, 50, -50)%20and%20
   date_time%20during%201935-01-01T00:00:00Z%20/%201935-12-31T23:59:59Z%20and%20
   observed_variable=85

### 3. Get a subset of the Observations table in CSV

http://<HOSTNAME>/geoserver/dyb/ows?service=WFS&version=1.0.0&
 request=GetFeature&
 typeName=dyb:observations_table_gis&
 outputFormat=csv&
 cql_filter=
   BBOX(location, -20, -80, 50, -50)%20and%20
   date_time%20during%201935-01-01T00:00:00Z%20/%201935-12-31T23:59:59Z%20and%20
   observed_variable=85
