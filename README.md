# Azure Services Hub
This template is intended to allow customers to evaluate alternative deployment options for Paloaltonetworks firewalls in a hub and spoke architecture. 

The diagram below indicates the deployment options.  


[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjharris10%2Fazure-svcs-hub%2Fmaster%2FazureDeploy.json?token=AZoiWUdo2qPkcTjMXpY8_KOkrP2aBqp_ks5ahJwcwA%3D%3D)

# Template Overview

![alt text](https://github.com/jharris10/azure-svcs-hub/blob/master/documentation/template-structure.png)

- The template structure is shown in the diagram.  Linked templates have been used to allow resources to be deployed into seperate resource groups and the user is also able to select the components to install.

- The resource groups must be created before the template is deployed.  This is an ARM Template limitation. 

- Future releases will allow the selection of Resourcegroups at runtime.

It includes following components:

1. One Internal Load Balancer (LB-Egress) - "Standard SKU"
- Two Paloaltonetworks Firewalls
  
2. One External TCP Load Balancer (LB-Ingress) -"Standard - SKU"
- Two Paloaltonetworks Firewalls
  
3. One Application Gateway
- Two Paloaltonetworks Firewalls
  


 The template allows selection of:
 - New or Existing VNET
 - BYOL or PAYG Licensing
 and creates all the infrastructure and appropriate UDRs.

 For information on how to bootstrap the VM-Series firewall running PAN-OS 8.1 and up in Azure see [Bootstrap Instructions](https://www.paloaltonetworks.com/documentation/81/virtualization/virtualization/bootstrap-the-vm-series-firewall/bootstrap-the-vm-series-firewall-in-azure#idd51f75b8-e579-44d6-a809-2fafcfe4b3b6)

 
 If bootstraping with default configuration file is used default credentials are:
 - Username: paloalto
 - Password: PaloAlt0!123!!

#  Deployment Instructions 

Create the resourece groups required. 
The current version of the template requires four resource groups.  The resource groups are stored in variables in the deployAzure.json template

1. Egress firewall resource group - Default 'egressfwrg'
- `az group create --name egressfwrg
    --location {azure region}
    `
2. Inbound TCP firewalls resource group - Default 'ipfwrg'
- `az group create --name ipfwrg
    --location {azure region}`

3. Application gateway firewall resource group - Default 'agggwfwrg'
- `az group create --name ipfwrg
    --location {azure region}`

Vnet related resources and the jumpbox will be created in the vnet resourcegroup.   The vnet resource group is selected in the deployment template.

Create the bootstrap folders and place the bootstrap files in the relevant folders.  

The template assumes the the we will be using folders under a common file share for all bootstrap accounts.

- Storgate Account
  - Fileshare
    - Egressfirewall Bootstrap
    - Ip firewall Bootstrap
    - Application Gateway Bootstrap