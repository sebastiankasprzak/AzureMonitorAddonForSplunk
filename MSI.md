# MSI Authentication
This section deals with setup process when using MSI authentication instead of SPN credentials.

## Overview
As an alternative to hardcoding SPN credentials in configuration files, Azure now provides alternative method of authentication to the Azure API using "Managed Service Identity".

Go to https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview to read more about how MSI works and it's use case and benefits.

MSI authentication is a recommended authentication option if the splunk instance responsible for collecting Azure Metrics is deployed on Azure VM. It also simplifies the configuration and authentication of this AddOn.

## Azure VM deployment
Before proceeding to next steps, you need to have Azure VM ready with splunk already installed on it.

Here is an example of ARM quick-start template to deploy Splunk in Azure VM: https://github.com/Azure/azure-quickstart-templates/tree/master/splunk-on-ubuntu

Once your VM is ready and splunk is installed on it, follow [[Installation | installation]] instructions to install this add-on and it's dependencies.

## Configuration

### Configuration Script

You can find installation script which will configure your Azure environment, use `-m` option to specify VM name on which splunk add-on has been installed.

Linux: https://github.com/Microsoft/AzureMonitorAddonForSplunk/blob/master/scripts/azure-setup.sh

Windows: WIP

### Manual Configuration

#### Enable MSI on VM

- navigate to the Vm in portal
- Navigate to `Configuration` section
- Select Yes under `Managed service identity` and save settings
- wait for deployment to complete

[[images/msi1.PNG]]

#### Configure KeyVault
- Create KeyVault within same Azure Subscription as the VM (or use already existing KeyVault)
- Navigate to `Access Policies` section
- Add new access policy, in `Select Principal` dialog you should now be able to find the Vm by it's name
- ensure the Access Policy specifies `Get` permission to Secrets
- ensure that the VM now appears in Access Policy and that the changes are saved

[[images/msi2.PNG]]

#### EventHub credentials
At this stage, although authentication to Azure API is now using MSI, the SAS credentials to authenticate with EventHub are still required, and it is best to store them in KeyVault. Follow [[Security #event-hub | security]] section to add EventHub SAS credentials to KeyVault

#### Add-on configuration

Splunk App can be configured as usual by following [[Splunk | configuration-of-splunk]] configuration page, however `SPNTenantID`, `SPNApplicationId`, and `SPNApplicationKey` fields can be left blank. When those fields are not filled in, then AddOn will try to use MSI for the purpose of authentication to API.