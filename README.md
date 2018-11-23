# PaloAlto firewall, fix deployment in existing AZURE cloud Virtual Network(V-NET)
Script by: <a href="https://www.linkedin.com/in/farshadrahaei">Farshad Rahaei</a>



Use this script to deploy Palo Alto firewall on existing Azure cloud virtual Network(V-NET), with addition of Premium_LRS SSD storage and Standard_DS3_v2 vm size.

In order to use this script you will need to have existing Azure Virtual Network(V-NET) and 3 Subnets for management, untrust and trust security zones.

Notes:
 - Change azureDeploy.parameters.json with your deployment configuration then update it in Azure "Edit Parameters".
 - Keep in mind to add security group to restrict access to your public PAN-Management subnet.
 
How to use this script:

# First Method:
# Using Azure Deployment Manager

Click on bellow button to redirect to azure cloud website and use this script for your deployemnt.

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ffarshadrahaei%2FPaloAltoNetworks%2Fmaster%2FazureDeploy.json)



# Second Method:
# Deploy ARM Template using Azure CLI in ARM mode

1. Download the two JSON files: azureDeploy.json and azureDeploy.parameters.json
2. Customize the azureDeploy.parameters.json file and then deploy it from your computer.
3. Install the latest <a href="https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/">Azure CLI</a> for your computer.</li>
4. Validate and deploy the ARM template:

``` azure
    azure login
    azure config mode arm
    azure  group  template  validate  -g YourResourceGroupName \
        -e  azureDeploy.json   -f  azureDeploy.parameters.json
    azure group create -v -n YourResourceGroupName -l YourAzureRegion  \
        -d  YourDeploymentLabel  -f azureDeploy.json -e azureDeploy.parameters.json
```

**Check the status of your deployment:**

- CLI: `azure vm show  -g YourResourceGroupName  -n YourDeploymentLabel`
- Azure Portal: Your Resource Group > Deployment or Alert Logs


