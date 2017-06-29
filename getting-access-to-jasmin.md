# Getting access to JASMIN

## Why get access to JASMIN?

Participants in the GLAMOD project will be developing a workflow that is primarily located on the JASMIN platform. This means that a large shared disk, known as a Group Workspace (GWS), will be accessible to project partners. If you are bringing data to JASMIN (and you are part of GLAMOD) or running code to work with the data you will need access to the GWS.

## Applying for access
In order to get access to the c3s311a_lot2 (GLAMOD) Group Workspace you will need to get access to the JASMIN platform and then apply for access to the appropriate resources. This is, unfortunately, a multi-step process but is fully documented [on the CEDA help site](http://help.ceda.ac.uk/category/158-getting-started).

You will need to pay attention to the following sections:

* **[Generate an SSH key pair](http://help.ceda.ac.uk/article/185-generate-ssh-key-pair)** - To enable login to JASMIN.
* **[Get a JASMIN account](http://help.ceda.ac.uk/article/4435-get-a-jasmin-account)** - General-purpose JASMIN account but without any specific resources accessible.
* **[Check network details](http://help.ceda.ac.uk/article/190-check-network-details)** – To ensure your institution is on our whitelist.
* **[Get a login account](http://help.ceda.ac.uk/article/161-get-login-account)** – Actually allowing SSH login to JASMIN.
* **[How to login](http://help.ceda.ac.uk/article/187-login)** – Instructions on how to login.
* **[Access to storage](http://help.ceda.ac.uk/article/176-storage)** – Worth a read for orientating yourself.

At this stage, it should be possible to login to the accounts portal and request access to the project Group Workspace from here:

[https://accounts.jasmin.ac.uk/services/group_workspaces/c3s311a_lot2/](https://accounts.jasmin.ac.uk/services/group_workspaces/c3s311a_lot2/)

You will need to wait for this request to be approved by the JASMIN manager for the project. This is currently Ag Stephens.

Once you have access you will be able to use `rsync` or `scp` to copy data to/from:

*Server:* **jasmin-xfer1.ceda.ac.uk**

*Directory:* `/group_workspaces/jasmin2/c3s311a_lot2/data/incoming/`

You will do this by creating an ssh-agent session which should then be picked up automatically by your rsync or scp process, e.g.:

```sh
$ exec ssh-agent $SHELL
$ ssh-add ~/.ssh/id_rsa_jasmin # or whatever you called you private key for JASMIN
$ rsync –rv <your_data_dir> <jasmin_userid>@jasmin-xfer1.ceda.ac.uk: /group_workspaces/jasmin2/c3s311a_lot2/data/incoming/
```

Alternatively, you can SSH in to our analysis servers to interact with the data:

*Servers:* **jasmin-sci1.ceda.ac.uk**, **jasmin-sci2.ceda.ac.uk**

*Directory:* `/group_workspaces/jasmin2/c3s311a_lot2/data/incoming/`

You will do this by creating an ssh-agent session and making an SSH connection to our login server (using the "-A" option) before going to one of the scientific analysis servers:

*NOTE: If you have already done these first two lines in your session then you don't need to repeat it.*
```sh
$ exec ssh-agent $SHELL
$ ssh-add ~/.ssh/id_rsa_jasmin # or whatever you called your private key for JASMIN
$ ssh -A <jasmin_userid>@jasmin-login1.ceda.ac.uk
$ ssh jasmin-sci2.ceda.ac.uk
# ...and go to the Group Workspace here:
$ cd /group_workspaces/jasmin2/c3s311a_lot2/data/incoming/
```

If you run into any problems with the above steps you can email support@ceda.ac.uk for assistance.
