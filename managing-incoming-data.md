# Managing incoming data

All raw incoming data from users should be compressed in a folder (named) and uploaded to the data holding directory on JASMIN:

`/group_workspaces/jasmin2/c3s311a_lot2/incoming`

Please name the data file and provide any metadata/readme documents available within the named comressed folder.

Please email [incoming_data@surfacetemperatures.org] with details of the uploaded data and provide a data inventory if available detailing:

* Station name
* Station Id
* WMO Id
* Latitude/Longitude
* Elevation
* FIPS Code
* ECVs available
* Data Start and End years for each ECV
* Any other variables available

The items that are essential: Station ID, Latitude/Longitude and elevation.

Please also provide *Data Usage Policy* information with supporting documentation in a word document or text doocument.

The data information will be added to the master source deck inventory and the relevant timescale station deck inventory. Once this has been achieved the data will be moved into the following directory and relevant timescale subdirectory:

```
/group_workspaces/jasmin2/c3s311a_lot2/data/level0
            land/monthly_data
            land/daily_data
            land/sub_daily_data
```

Following data harmonisation, quality control and homogeneity checks the data will be made available based on the source Data Usage Policy. We will try to ensure that the data source is cited whenever the data are used.

## Keeping track of the data we have

I have written some instructions on using the checkm tool to generate manifest files here:

[https://github.com/glamod-test/glamod-dm/tree/master/manifests](https://github.com/glamod-test/glamod-dm/tree/master/manifests/example/)

The instructions should show you how to install checkm into a python environment and then run the script.

Here is an example of a data directory and the resulting manifest file generated when you run the script:

[https://github.com/glamod-test/glamod-dm/tree/master/manifests/example/](https://github.com/glamod-test/glamod-dm/tree/master/manifests/example/)

## Resources

Some resources that might be useful:

NCAS/CEDA ISC course Git introduction:

[https://github.com/ncasuk/ncas-isc/blob/master/shell/presentations/01_git2.pptx/blob/master/shell/presentations/01_git2.pptx](https://github.com/ncasuk/ncas-isc/blob/master/shell/presentations/01_git2.pptx/blob/master/shell/presentations/01_git2.pptx)

[Return to index](README.md)
