# Transferring data to/from JASMIN:

In-depth information about data transfer on JASMIN can be found on the CEDA help site:
http://help.ceda.ac.uk/category/217-data-transfer

## Quick example

To copy a file to your home directory (In mobaxterm):

```sh
scp astephen@jasmin-xfer1.ceda.ac.uk:/group_workspaces/jasmin2/c3s311a_lot2/data/incoming/marine_what_am_i/2015/01/usaf-swo-03_REPLACE_s20150114_e20150203_c20170106220346.tar .
```

To copy directories use "-r", e.g.:

```sh
scp -r astephen@jasmin-xfer1.ceda.ac.uk:/group_workspaces/jasmin2/c3s311a_lot2/data/incoming/marine_what_am_i/2015/01 .  
```