# Variables for your state backend
STATE_RG="tfstate-rg"
STATE_LOCATION="germanywestcentral"
STATE_STORAGE_ACCOUNT="tfstatesa$RANDOM" # Add randomness to make it globally unique
STATE_CONTAINER="sample-azure-function-python-tfstate"

# 1. Create a dedicated resource group for your state file
az group create --name $STATE_RG --location $STATE_LOCATION

# 2. Create a storage account inside that group
az storage account create --name $STATE_STORAGE_ACCOUNT --resource-group $STATE_RG --location $STATE_LOCATION --sku Standard_LRS

# 3. Create a blob container where the state file will live
az storage container create --name $STATE_CONTAINER --account-name $STATE_STORAGE_ACCOUNT


az ad sp create-for-rbac --name "sample-azure-function-python-app-sp" --sdk-auth