# Azure Virtual Machines

## Overview:
- **Definition:** Azure Virtual Machines (VMs) offer Infrastructure as a Service (IaaS) by providing virtualized servers in the cloud, allowing customization of software and hosting configurations.
- **Key Benefits:** 
  - Total control over the operating system (OS).
  - Ability to run custom software.
  - Flexibility of virtualization without managing physical hardware.

## Provisioning VMs:
- **Image Selection:** Users can choose from preconfigured VM images for rapid provisioning, containing OS and software templates.
- **Scaling Options:** 
  - **Single VMs:** Suitable for testing, development, or minor tasks.
  - **Scale Sets:** Manage groups of load-balanced VMs for high availability, scalability, and redundancy.

## Virtual Machine Scale Sets:
- **Definition:** Automates management, configuration, and scaling of a group of identical, load-balanced VMs.
- **Features:** 
  - Auto-scaling based on demand or schedule.
  - Centralized management and updates.
  - Deployment of load balancer for efficient resource utilization.
- **Use Cases:** Ideal for compute-intensive, big data, and container workloads.

## Virtual Machine Availability Sets:
- **Definition:** Ensures resiliency and high availability by grouping VMs based on update and fault domains.
- **Update Domain:** Groups VMs for staggered updates, minimizing downtime.
- **Fault Domain:** Distributes VMs across different power and network resources to prevent single points of failure.
- **Cost:** No additional cost for configuring availability sets; pay only for VM instances.

## Common Use Cases for VMs:
- **Testing and Development:** Provides flexibility to create different OS and application configurations, with easy deletion after use.
- **Running Applications in the Cloud:** Economical option for handling fluctuating demand, paying only for resources used.
- **Extending Datacenter to the Cloud:** Enables running applications like SharePoint in Azure VMs, offering cost-effective deployment.
- **Disaster Recovery:** Cost-effective disaster recovery solution, allowing quick deployment of critical applications in Azure during datacenter failures.

## VM Resources:
- **Provisioning Options:** Users can customize VM resources including size, storage disks, and networking configurations.
  - Size: Purpose, number of processor cores, and RAM.
  - Storage Disks: Hard disk drives, solid-state drives, etc.
  - Networking: Virtual network, public IP address, and port configuration.



# Excercise

## 1: Create Linux VM & Install Nginx

### 1. Run the following from cloud shell to create a VM.
```ps
az vm create --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --name my-vm --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys
```
- `az vm create` is used to create a vm, and then we provide the information such as the resource-group, name , image and username.
- we can use `az vm list` to list all VMs.
- we can use `az vm list-ip-address` to get the IP addresses for our VM.
```ps
nurbxfit [ ~ ]$ az vm list-ip-addresses --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --name my-vm
[
  {
    "virtualMachine": {
      "name": "my-vm",
      "network": {
        "privateIpAddresses": [
          "10.0.0.4"
        ],
        "publicIpAddresses": [
          {
            "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Network/publicIPAddresses/my-vmPublicIP",
            "ipAddress": "13.88.175.178",
            "ipAllocationMethod": "Static",
            "name": "my-vmPublicIP",
            "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
            "zone": null
          }
        ]
      },
      "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8"
    }
  }
]
```
- we can show details about our vm using this command 
```ps
az vm show --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --name my-vm
```

- we can get help by using this command 
```ps
az vm --help
```

### 2. Run the following from the cloud shell to configure nginx.
```ps
az vm extension set --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm --name customScript --publisher Microsoft.Azure.Extensions --version 2.1 --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```
- this will add extension into our vm, the extension is from the scrip on a github repository.
- we can get help by using this command 
```ps
az vm extension --help
```

**List Down Extensions**

- we can list down the extenstion using `az vm extension list`

Example before we run `az vm extension set` 
```ps
nurbxfit [ ~ ]$ az vm extension list --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm
[
  {
    "autoUpgradeMinorVersion": true,
    "enableAutomaticUpgrade": false,
    "forceUpdateTag": null,
    "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/OmsAgentForLinux",
    "instanceView": null,
    "location": "westus",
    "name": "OmsAgentForLinux",
    "protectedSettings": null,
    "protectedSettingsFromKeyVault": null,
    "provisionAfterExtensions": null,
    "provisioningState": "Succeeded",
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
    "settings": {
      "workspaceId": "dc8a3fb0-bd7c-4f8a-98c7-5712aeb14742"
    },
    "suppressFailures": null,
    "tags": null,
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "typeHandlerVersion": "1.0",
    "typePropertiesType": "OmsAgentForLinux"
  }
]
```

Example After we set extension 
```ps 
nurbxfit [ ~ ]$ az vm extension list --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm
[
  {
    "autoUpgradeMinorVersion": true,
    "enableAutomaticUpgrade": null,
    "forceUpdateTag": null,
    "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/customScript",
    "instanceView": null,
    "location": "westus",
    "name": "customScript",
    "protectedSettings": null,
    "protectedSettingsFromKeyVault": null,
    "provisionAfterExtensions": null,
    "provisioningState": "Succeeded",
    "publisher": "Microsoft.Azure.Extensions",
    "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
      ]
    },
    "suppressFailures": null,
    "tags": null,
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "typeHandlerVersion": "2.1",
    "typePropertiesType": "customScript"
  },
  {
    "autoUpgradeMinorVersion": true,
    "enableAutomaticUpgrade": false,
    "forceUpdateTag": null,
    "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/OmsAgentForLinux",
    "instanceView": null,
    "location": "westus",
    "name": "OmsAgentForLinux",
    "protectedSettings": null,
    "protectedSettingsFromKeyVault": null,
    "provisionAfterExtensions": null,
    "provisioningState": "Succeeded",
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
    "settings": {
      "workspaceId": "dc8a3fb0-bd7c-4f8a-98c7-5712aeb14742"
    },
    "suppressFailures": null,
    "tags": null,
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "typeHandlerVersion": "1.0",
    "typePropertiesType": "OmsAgentForLinux"
  }
]
```
noticed now at top, we have another extension, we added just now.
```json
  "name": "customScript",
```

**Show Extension Information**

- if we know our extension name we can filter and show the information by running this command 

```ps
nurbxfit [ ~ ]$ az vm extension show --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm --name "customScript"
{
  "autoUpgradeMinorVersion": true,
  "enableAutomaticUpgrade": null,
  "forceUpdateTag": null,
  "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/customScript",
  "instanceView": null,
  "location": "westus",
  "name": "customScript",
  "protectedSettings": null,
  "protectedSettingsFromKeyVault": null,
  "provisionAfterExtensions": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.Extensions",
  "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
  "settings": {
    "fileUris": [
      "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
    ]
  },
  "suppressFailures": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "2.1",
  "typePropertiesType": "customScript"
}
```

**Remove Extension**

- we can delete the extension using the command `az vm extension delete`
```ps
az vm extension delete --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm --name "customScript"
```
- to verify that we indeed deleted the extension we can list it again.

```ps
nurbxfit [ ~ ]$ az vm extension list --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm
[
  {
    "autoUpgradeMinorVersion": true,
    "enableAutomaticUpgrade": false,
    "forceUpdateTag": null,
    "id": "/subscriptions/651da11b-7757-4742-ac91-148e47c2869b/resourceGroups/learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8/providers/Microsoft.Compute/virtualMachines/my-vm/extensions/OmsAgentForLinux",
    "instanceView": null,
    "location": "westus",
    "name": "OmsAgentForLinux",
    "protectedSettings": null,
    "protectedSettingsFromKeyVault": null,
    "provisionAfterExtensions": null,
    "provisioningState": "Succeeded",
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "resourceGroup": "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8",
    "settings": {
      "workspaceId": "dc8a3fb0-bd7c-4f8a-98c7-5712aeb14742"
    },
    "suppressFailures": null,
    "tags": null,
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "typeHandlerVersion": "1.0",
    "typePropertiesType": "OmsAgentForLinux"
  }
]
```
- if we were to run show command, it will show an error ResourceNotFound
```ps
nurbxfit [ ~ ]$ az vm extension show --resource-group "learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8" --vm-name my-vm --name "customScript"

(ResourceNotFound) The Resource 'Microsoft.Compute/virtualMachines/my-vm/extensions/customScript' under resource group 'learn-f6dbfeb3-c6cc-48a3-a7fc-9537bd05cfd8' was not found. For more details please go to https://aka.ms/ARMResourceNotFoundFix
Code: ResourceNotFound
```

End Note: 
- when we set the extension we specify the settings to run the `configure-nginx.sh` script from the github. 
- The content of that [script](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh) is as below.

```sh
#!/bin/bash

# Update apt cache.
sudo apt-get update

# Install Nginx.
sudo apt-get install -y nginx

# Set the home page.
echo "<html><body><h2>Welcome to Azure! My name is $(hostname).</h2></body></html>" | sudo tee -a /var/www/html/index.html
```