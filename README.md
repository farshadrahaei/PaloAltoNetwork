# PaloAlto Networks Firewall deployement in Azure Cloud
# Fixed deplyment in existing Azure Virtual Network (V-NET)
Deploying Palo Alto firewall on existing Azure virtual Network(V-NET), with addition of Premium_LRS SSD storage and Standard_DS3_v2 vm size.
In order to use this script you will need to have existing Azure Virtual Network(V-NET) and 3 Subnets.
Keep in mind to add security group to restrict access to your public PAN-Management subnet.

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ffarshadrahaei%2FPaloAltoNetworks%2Fmaster%2FazureDeploy.json)

## Deploy ARM Template using Azure CLI in ARM mode

1. Download the two JSON files: azureDeploy.json and azureDeploy.parameters.json
1. Customize the azureDeploy.parameters.json file and then deploy it from your computer.
1. Install the latest <a href="https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/">Azure CLI</a> for your computer.</li>
1. Validate and deploy the ARM template:

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
