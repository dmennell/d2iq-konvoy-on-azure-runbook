# D2iQ Konvoy On Microsoft Azure Runbook
This is a simple quickstart guide for deploying D2iQ Konvoy Kubernetes on Azure Public Cloud.  This is by no means an exhaustive documentation.  It is merely a quick start on what is needed to get up and running with Konvoy on Azure.  Complete documentation for deploying Konboy Kubernetes on Azure can be found here:
https://docs.d2iq.com/ksphere/konvoy/latest/install/install-azure/



## Azure Credentials and CLI Setup
To successfully deploy a Konvoy cluster on Azure, you will first need to install the Azure CLI, configure your credentials, and successfully login through the CLI.  Instructions can be found here:
https://github.com/dmennell/d2iq-konvoy-on-azure-runbook/blob/master/azure-credentials-config.md

## Konvoy Install Node SetupSetup
Process you need to follow to get the files in place prior to running the install.

1. Ensure that the typical prerequisites are in place: Docker and Kubectl 
Create a working directory somewhere.  This directory name should not contain capitol letters, underscore, or spaces.
2. Navigate to it in the Terminal Emulator of your choice (Terminal, iTerm2, VScode, etc).
3. Get the Konvoy binaries and decompress them as usual (if you choose, you can add the binaries to your PATH)
4. Move the Four files to your working Directory.  As this is a testing exercise, we will skip adding the directory to the path and access them directly by calling "./konvoy" directly
5.  Make sure that the Konvoy binaries and tar files can be bind mounted into Docker containers.

## Yo VIP... Let's Kick It

**Initialize The Deployment Like Normal:**  this time, specify the provisioner as "Azure".  Again, as this is for testing purposes, we have not added this location to the path, and Konvoy will need to be run with "./"
```
./konvoy init --provisioner=azure
```

**Review the Azure-Provisioned "config.yaml"** and how differs from AWS (nodes, storage, networking, etc) and modify as necessary (by default, Konvoy provisions 6 worker nodes for an azure Kubernetes cluster)
```
vi cluster.yaml
```

**Login to Azure via CLI** (See the "Azure Credentials" section for help)
```
az login
```
You will be presented with a browser page on which to enter your credentials.  Fill them in and return to your command line.  You should see a set of permissions for your session as a response.

**Deploy It !!!** (Insert “-y” to skip the confirmation)
```
./konvoy up -y
```

**Go Get Some Coffee...** you know this is gonna take a while, and a watched pot never boils.  
```
Addons deployed successfully!
Run `./konvoy apply kubeconfig` to update kubectl credentials.
Navigate to the URL below to access various services running in the cluster.
  https://13.87.153.150/ops/landing
And login using the credentials below.
  Username: loving_bohr
  Password: UMIbVIBh3UleE3B55WoQNX8HmCQR21IMVBrfhMXDcZTLXUncrG7Hr0U9KuxVEVvr

If the cluster was recently created, the dashboard and services may take a few minutes to be accessible.
```

## Deployment Notes

**Credentials Rights**
The Konvoy provisioner requires that specific rights be associated with your Azure credentials.  Please ensure that your credentials have "contributor" rights associated with them.  If you are unsure, please see below for a link to a guide to setting up your credentials:

**Credentials Quota**
As many of you will be using MSDN Azure credits for your deployments, please ensure that you have the available quota to deploy Konvoy.  If you do not, you will receive an error stating that you do not have the available resource quota.

**Install Errors**
As with all other Konvoy deployments, if there is an error, it could be a race condition occured, and you can simply run the "up" process again to pick up where you left off.
```
./konvoy up -y
```
If you have already made it to the "Addons" section of the deployment, and the install errors out, you can skip the full "up" process and skip to deploying the addons:
```
./konvoy deploy addons -y
```

**Apply Kubeconfig Not Working**
If you are getting an error message that Konvoy cannot update the kubeconfig file, because a duplicate entry already exists, you will need to . "force-overwrite" the file by running the following command:
```
./konvoy apply kubeconfig --force-overwrite
```

**It Takes a While**
Konvoy on Azure takes a-lot longer to provision than on AWS or Google (roughly 30 minutes in my experience).  This is a function of the time it takes Azure to provision the resources, not Konvoy.  Please be patient.

**Verified Developer Error**
If you are using OSX Catalina, there is a good chance you will get an error message about this app being from an un verified developer.  Click cancel.  Go to the System Preferences:Security section.  Click the "Allow Anyway" button.  Run your command again and select "OK".  You should be good to proceed

Have Fun!


