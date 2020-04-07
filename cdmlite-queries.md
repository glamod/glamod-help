# CDMlite queries

## CDS Form: Land

### Land fields

The Land CDS form will have the following selections:

- frequency [1]:
  - Monthly
  - Daily
  - Sub-daily
 
- variable [1..many]:
  - Dew Point Temperature
  - Accumulated Precipitation
  - Fresh Snow
  - Snow Depth
  - Snow Water Equivalent
  - Air Pressure
  - Air Pressure At Sea Level
  - Air Temperature
  - Wind From Direction
  - Wind Speed
  
- intended_use [1]:
  - Non-commercial
  - Commercial
  
- data_quality [1]:
  - Quality-controlled
  - All data
  
- year [1]:
  - 1761
  - ...
  - 2018
  
- month [1]:
  - Jan
  - ...
  - Dec
  
- day [1..many]: # Hide if frequency == "Monthly"
  - 01
  - ...
  - 31
  
- hour [1..many]: # Hide if frequency in ("Monthly", "Daily")
  - 00
  - ...
  - 23
  
- bounding_box [1]:
  - standard widget
  
- format [1]:
  - CSV (zipped)

### Land WFS template

The basic query template is as follows:

```
http://glamod2.ceda.ac.uk/wfs/?request=GetFeature&typename=observations&outputFormat={FORMAT}&cql_filter=
  date_time%20DURING%20{YEAR}-{MONTH}-{START_DAY}T{START_HOUR}:00:00Z/
                       {YEAR}-{MONTH}-{END_DAY}T{END_HOUR}:59:59Z
                       
  %20AND%20observed_variable%20IN%20({VARIABLES_COMMA_SEPARATED})
  %20AND%20report_type={REPORT_TYPE}
  %20AND%20platform_type%20NOT%20IN%20(2,5)
  %20AND%20quality_flag={QUALITY_FLAG}
  %20AND%20data_policy_licence={DATA_POLICY}
```

For example, here are a set of inputs mapped to a valid query:

INPUTS: 
 - frequency: Daily
   - maps to: REPORT_TYPE: "3"
 - variable: (Accumulated Precipitation, Air Temperature)
   - maps to: VARIABLES_COMMA_SEPARATED: "44,85"
 - intended_use: "Non-commercial"
   - maps to: DATA_POLICY: "1"
 - data_quality: Quality-controlled
   - maps to: QUALITY_FLAG: "0"
 - Time components:
   - year: 1999, month: 06, day: 01
   - maps to:
     - YEAR: "1999"
     - MONTH: "06"
     - START_DAY and END_DAY: "01"
     - START_HOUR (default): "00"
     - END_HOUR (default): "23"
- format: "csv"
  - maps to: FORMAT: "csv"

Injecting these values into the template gives:
```
http://glamod2.ceda.ac.uk/wfs/?request=GetFeature&typename=observations&outputFormat=csv&cql_filter=
  date_time%20DURING%201999-06-01T00:00:00Z/
                       1999-06-01T23:59:59Z
                       
  %20AND%20observed_variable%20IN%20(44,85)
  %20AND%20report_type=3
  %20AND%20platform_type%20NOT%20IN%20(2,5)
  %20AND%20quality_flag=0
  %20AND%20data_policy_licence=1
```

As a single URL (with `&count=100` added):

http://glamod2.ceda.ac.uk/wfs/?request=GetFeature&typename=observations&outputFormat=csv&cql_filter=date_time%20DURING%201999-06-01T00:00:00Z/1999-06-01T23:59:59Z%20AND%20observed_variable%20IN%20(44,85)%20AND%20report_type=3%20AND%20platform_type%20NOT%20IN%20(2,5)%20AND%20quality_flag=0%20AND%20data_policy_licence=1&count=100

If we remove the `&count=100` specifier then we get 34,000 records:

http://glamod2.ceda.ac.uk/wfs/?request=GetFeature&typename=observations&outputFormat=csv&cql_filter=date_time%20DURING%201999-06-01T00:00:00Z/1999-06-01T23:59:59Z%20AND%20observed_variable%20IN%20(44,85)%20AND%20report_type=3%20AND%20platform_type%20NOT%20IN%20(2,5)%20AND%20quality_flag=0%20AND%20data_policy_licence=1

NOTES:
 - quality_flag:
   - 0: means "passed QC"
   - 1: means "failed QC"
 - data_policy_licence:
   - 0: means open for commercial use
   - 1: means WMO Essential licence
 
