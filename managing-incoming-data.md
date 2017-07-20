# Managing incoming data

All raw incoming data from users should be uploaded to the data holding directory:

`/group_workspaces/jasmin2/c3s311a_lot2/data/incoming`

Please name the data file and provide any metadata/readme documents available.

Please email [incoming_data@surfacetemperatures.org] with details of the uploaded data and provide a data inventory if available detailing:

* Station name
* Station Id
* Latitude/Longitude
* Elevation
* FIPS Code
* ECVs available
* Data Start and End years for each ECV
* Any other variables available

Please also provide *Data Usage Policy* information with supporting documentation.

The data information will be added to the master source deck inventory and the relevant timescale station deck inventory. Once this has been achieved the data will be moved into the following directory and relevant timescale subdirectory:

```
/group_workspaces/jasmin2/c3s311a_lot2/data/stage1_raw_data/
            monthly_data/
            daily_data/
            sub_data/
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
