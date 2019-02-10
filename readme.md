# Windows Server 2016 - Standalone Domain Controller Template


GitHub repository offers test platform who wants to deploy quickly Active Directory Environment which will be placed on Windows Server 2016 OS for Azure deployments. All of the templates in this repository have been developed for who needs this structure. This repository contains just Standalone Active Directory deployment templates that have been tested. The templates for Microsoft Learning Partner who wants to demonstrate quickly Azure Resource Manager Templates

Description | Link | Visualize
--- | --- | ---
Full deploy - Virtual Network, WS 2016 - New AD Forest  | <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhasangural%2Fazure-dc-2016%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a> | <a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhasangural%2Fazure-dc-2016%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="http://armviz.io/visualizebutton.png"/></a>

 # Deploys the following infrastructure:

 This template needs parameters which will be used for deployment process.

* envName      : Please provide your environment name. It might be like this : Microsoft > msft.
* vNETAddress  : Please provide your Virtual Network Address Prefix. It should be like this : 192.168.0
* userName     : Please provide your windows user name. It should be different from Administrator: Mike
* userPassword : Please provide your windows  password. Example : Mike!s201
* domainName   : Please provide your domain name. It might be like : msft.com

This template allows you to create these resources.

* Virtual Machine - ADDS Service
  * Network Security Group with RDP Rule
  * Public Ip Address - Static
  * Desired State Configuration Extension - ADDS
  * BGInfo Extension 
  * Diagnostic Storage
* Virtual Network
  * 2 subnets: Application, Management
  * DNS Server : ADDS Server


Also you can deploy this template with the Powershell. Before you have to login with your Azure Admin Account on the Azure Powershell. However, you can use Azure Cloud Shell.

```PowerShell
# --- Set resource group name and create
$ResourceGroupName = "pr-prod-rg"
New-AzureRmResourceGroup -Name $ResourceGroupName -Location "West Europe" -Force

# --- Deploy infrastructure
$DeploymentParameters = @{
    envName = "msft"
    vNETAddress = "172.10.0"
    userName = "prAdmin"
    userPassword = "mike!s10!q"
    domainName = 'msft.com'

}

New-AzureRmResourceGroupDeployment -Name "deployment-01" -ResourceGroupName $ResourceGroupName -TemplateFile .\examples\example-linked-template.json @DeploymentParameters
```
