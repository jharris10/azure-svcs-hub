# azure-svcs-hub

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjharris10%2Fazure-svcs-hub%2Fmaster%2FIgniteDeploy.json?token=AZoiWUdo2qPkcTjMXpY8_KOkrP2aBqp_ks5ahJwcwA%3D%3D)

![alt text](https://raw.githubusercontent.com/jharris10/azure-svcs-hub/blob/master/documentation/template-structure.png)

![alt text](https://raw.githubusercontent.com/jharris10/azure-fw-east-west/master/Architecture-Diagram.png)

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjharris10%2Fshared-fw-ref-architecture%2Fmaster%2FazureDeploy.json)

This template automates deployment of firewall LB sandwich environment for Egress Security.
It includes following components:

- One Internal Load Balancer (LB-Egress) - "Standard SKU"
- Two Paloaltonetworks Firewalls
  
- One External TCP Load Balancer (LB-Ingress) -"Standard - SKU"
- Two Paloaltonetworks Firewalls
  
- One Application Gateway
- Two Paloaltonetworks Firewalls
  
- Multiple Subnets and UDRs to support the traffic flow

Each loadbalancer + firewall is deployed into its own resourcegroup.
The resource groups must be created before the template is deployed.  This is an ARM
Template limitation. Future releases will allow the selection of Resourcegroups at runtime.

 The template allows selection of:
 - New or Existing VNET
 - Bootstraping
 - BYOL or PAYG Licensing
 and creates all the infrastructure and appropriate UDRs.

 For information on how to bootstrap the VM-Series firewall running PAN-OS 8.1 and up in Azure see [Bootstrap Instructions](https://www.paloaltonetworks.com/documentation/81/virtualization/virtualization/bootstrap-the-vm-series-firewall/bootstrap-the-vm-series-firewall-in-azure#idd51f75b8-e579-44d6-a809-2fafcfe4b3b6)

 
 If bootstraping with default configuration file is used default credentials are:
 - Username: paloalto
 - Password: PaloAlt0!123!!