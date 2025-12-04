# SimpleBicep

This repo contains a minimal Bicep template for creating a resource group at the subscription scope.

## Deploy the Resource Group

1. Install the latest [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) and sign in with `az login`.
2. From the repo root, deploy with the provided parameter file (edit values in `main.parameters.json` first if needed):

	 ```pwsh
	 az deployment sub create \ 
	 	 --location westus2 \ 
	 	 --template-file main.bicep \ 
	 	 --parameters @main.parameters.json
	 ```

	 ```pwsh
	 # Optional: override or add parameters inline
	 az deployment sub create \ 
	 	 --location westus2 \ 
	 	 --template-file main.bicep \ 
	 	 --parameters @main.parameters.json "tags={environment:'dev'}"
	 ```

3. Verify the deployment in the Azure Portal or via `az group show --name <rg-name>`.

> The template (`main.bicep`) exposes `resourceGroupName`, `location`, and `tags` parameters and outputs the resulting `resourceGroupId` for chaining into downstream deployments.
