# Application Security Group (ASG) Creation

## Overview
In this task, we create an Application Security Group (ASG) to allow secure communication within a specific group of resources.

## Steps

1. **Open the Azure Portal**:
   - Navigate to the Azure portal [here](https://portal.azure.com).

2. **Create an ASG**:
   - Search for and select `Application security groups`.
   - Click on `+ Create`.

3. **Fill in the Basic Information**:
   - **Subscription**: Select your subscription.
   - **Resource Group**: Select `vnet-rg`.
   - **Name**: Enter `asg-web`.
   - **Region**: Select `North Europe`.

4. **Review and Create**:
   - Click `Review + Create`.
   - After validation, click `Create`.

5. **Deployment**:
   - Wait for the deployment to complete, and confirm that the ASG has been successfully created.

## JSON Reference

You can also create this ASG via the Azure CLI or using the JSON template provided below:

```json
{
  "name": "asg-web",
  "location": `North Europe`,
  "properties": {}
}
