# Configure Azure Credentials For Konvoy
To successfully deploy a Konvoy cluster on Azure, you must have a properly configured Azure credentials and CLI.

Here is a link to the official D2iQ documents focused on configuring the Azure CLI:
https://github.com/mesosphere/konvoy/blob/azure/docs/site/install/install-azure/index.md#prerequisites


## Configure Azure Credentials
Azure credentials must be configured with specific permissions in order to deploy Konvoy Kubernetes.  In addition.

1.  Your account must be configured as a “contributor “ in whatever account group you are assigned.
    * Your Azure administrator must run the following command to give you further specific rights.  Make sure to insert your user credentials in the appropriate place below.
```
az role assignment create —assignee <insert-your-azure-userid-here> —role “User Access Administrator”
```


## Install Azure CLI
Install the Azure CLI via HomeBrew.  If you have not already installed “python 3”, it will be installed as a dependency.
```
brew update && brew install azure-cli
```

Complete instructions for the Azure CLI can be found below:

* OSX URL: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest
* Linux URL: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest


## Verify Azure Credentials and Login
In a compatible browser, go to the following address and attempt to login with your credentials.  This will give you a clue as to whether your credentials are valid.
<https://portal.azure.com>

From the command line, run the following:
```
az login
```
A browser window will open and prompt you for your user ID and Password if not already done so.  If credentials are cached, click the appropriate one.  If not cached, enter them.  If you are logged in correctly, you should see something resembling the text block below.
```
=> az login
Note, we have launched a browser for you to login. For old experience with device code, use "az login --use-device-code"
You have logged in. Now let us find all the subscriptions to which you have access...
[
  {
    "cloudName": "AzureCloud",
    "id": "thisIsNotTheIdYouAreLookinForMoveAlong",
    "isDefault": true,
    "name": "whatIsYourName",
    "state": "Enabled",
    "tenantId": "getYourOwnTennantID-12345",
    "user": {
      "name": "azureCredentialsRemovedToProtectTheInnocent",
      "type": "user"
    }
  }
```
 

## Verify Permissions Are Set Correctly through CLI
Now we will verify through the CLI that your credentials are set properly.

In the Terminal, run the following command entering your Azure user name where appropriate:
```
az role assignment list --assignee <YOUR-USER-LOGIN>
```

If your credentials are set properly, you should see the following lines referenced (3rd from the bottom of their respective paragraphs):
```
"roleDefinitionName": "User Access Administrator"
"roleDefinitionName": "Contributor"
```

That's it... If all went well, you should be ready to do what you came here to do :-)


## Notes
none yet
