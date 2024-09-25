# spring-boot-github-actions-docker-img-azure-acr
Demo project spring boot with github actions, docker image push to azure acr

## Azure ACR Creation Details
- Show subscriptionid
```
az account show --query id
```

- Create a service prinicipal using below command or Create Azure Portal
```
az ad sp create-for-rbac --name "terraform-sp" --role="Contributor" --scopes="/subscriptions/<subscriptionid>" --sdk-auth
```

- Create a Resource group or Create Azure Portal
```
az group create --name my_resource_group --location eastus
```

- Create ACR
```
az acr create --resource-group my-resource-group --name nagarajaracrregistry --sku Basic --admin-enabled true
```

- Get ACR Details and use login server details
```
az acr show --name nagarajaracrregistry --query "loginServer"
```

- Get userName of acr
```
az acr credential show --name nagarajaracrregistry --query "username"
```

- Get password for acr
```
az acr credential show --name nagarajaracrregistry --query "passwords[0].value"
```

- Create a azure container group or Create Azure Portal
```
az container create \
  --resource-group my_resource_group \
  --name my-container-group-2 \
  --image acrloginserverdetails/my-azure-app:latest \
  --cpu 1 \
  --memory 1.5 \
  --ports 8080 \
  --ip-address public \
  --dns-name-label nagarajarazure-app \
  --environment-variables JAVA_OPTS="-Xmx512m" \
  --registry-login-server acrloginserverdetails \
  --registry-username nagarajaracrregistry \
  --registry-password {Enter acr password}
```

## Create GitHub Actions
- Click on the Actins on top navigation -> Give name and select predefined config then commit the changes.

## Create Secrete in GitHub
- Go to Settings on top navigation -> Click on Secretes and Variables then Create New Repo Secrete on by one.
  - ACR_LOGIN_SERVER
  - ACR_USERNAME
  - ACR_PASSWORD




