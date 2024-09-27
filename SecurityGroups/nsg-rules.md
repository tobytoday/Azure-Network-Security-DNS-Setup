```markdown
# Network Security Group (NSG) Rules Configuration

## Overview
In this task, we create a Network Security Group (NSG) and configure inbound and outbound rules to control traffic to and from the associated resources.

## Steps

### 1. Create an NSG

1. **Open the Azure Portal**:
   - Navigate to the Azure portal and search for `Network Security Groups`.

2. **Create a New NSG**:
   - Click on `+ Create` to create a new Network Security Group.
   - Fill in the required fields:
     - **Subscription**: Select your subscription.
     - **Resource Group**: Select `vnet-rg`.
     - **Name**: Enter `myNSG`.
     - **Region**: Select `North Europe`.

3. **Review and Create**:
   - Click `Review + Create`.
   - After validation, click `Create`.

4. **Associate with Subnet**:
   - After deployment, go to the NSG resource.
   - Under `Settings`, select `Subnets` and click `Associate`.
   - Select the `CoreServicesVnet` and the `SharedServicesSubnet`.

### 2. Configure Inbound Rules

1. **Allow ASG Traffic**:
   - Go to the NSG resource and select `Inbound security rules`.
   - Click `+ Add`.
   - Configure the inbound rule:
     - **Source**: Application Security Group
     - **Source ASG**: `asg-web`
     - **Source port ranges**: `*`
     - **Destination**: Any
     - **Service**: Custom
     - **Destination port ranges**: `80, 443`
     - **Protocol**: TCP
     - **Action**: Allow
     - **Priority**: 100
     - **Name**: `AllowASG`

2. **Outbound Rule to Deny Internet**:
   - Go to `Outbound security rules` and add a new rule.
   - Configure the outbound rule:
     - **Source**: Any
     - **Source port ranges**: `*`
     - **Destination**: Service Tag
     - **Destination service tag**: Internet
     - **Destination port ranges**: `8080`
     - **Protocol**: Any
     - **Action**: Deny
     - **Priority**: 4096
     - **Name**: `DenyAnyCustom8080Outbound`

## JSON Reference

The following JSON template can be used to automate the NSG creation and rule configuration:

```json
{
  "name": "myNSGSecure",
  "location": "East US",
  "properties": {
    "securityRules": [
      {
        "name": "AllowASG",
        "properties": {
          "priority": 100,
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80,443",
          "sourceApplicationSecurityGroups": [
            {
              "id": "[resourceId('Microsoft.Network/applicationSecurityGroups', 'asg-web')]"
            }
          ],
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "direction": "Inbound"
        }
      },
      {
        "name": "DenyAnyCustom8080Outbound",
        "properties": {
          "priority": 4096,
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "8080",
          "destinationAddressPrefix": "Internet",
          "access": "Deny",
          "direction": "Outbound"
        }
      }
    ]
  }
}
