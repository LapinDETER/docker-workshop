# Deploy our Container to Azure using Azure CLI 2.0 

First we need to install the Azure CLI 2.0 

But wait that is based on python, and I don't want python on my machine

Luckily there a docker image: https://hub.docker.com/r/azuresdk/azure-cli-python/ 

Lets run that

`
docker run -v c:/temp:/root -it microsoft/azure-cli
`

Boom now you have a Azure CLI 2.0 prompt without even installing anything

Now lets create some azure resources 

Inside the Azure CLI bash shell 

```
az login 

az account set --subscription <subscription-id>

az group create --name dockertest --location westeurope
```

To create a Azure Container Instance which we need next

`
az acr create --name skpdk --location westeurope --resource-group dockertest --sku Basic
`

To enable the admin account

`
az acr update -n skpdk --admin-enabled true
`

Now to get the password

`
az acr credential show --name skpdk --query passwords[0].value
`


