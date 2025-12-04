# SimpleBicep

This repo contains a minimal Bicep template for creating a resource group at the subscription scope.

## Deploy the Resource Group

1. Install the latest [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) and sign in with `az login`. If you prefer running in [Azure Cloud Shell](https://learn.microsoft.com/azure/cloud-shell/overview), clone the repo and switch into it first:

	```bash
	git clone https://github.com/cdonlan/SimpleBicep.git
	cd SimpleBicep
	```
2. From the repo root, deploy with the provided parameter file (edit values in `main.parameters.json` first if needed). When using PowerShell, wrap the `@file` reference in quotes so it is not treated as splatting:

	 ```pwsh
	 az deployment sub create `
	   --location westus2 `
	   --template-file main.bicep `
	   --parameters '@main.parameters.json'
	 ```

	 ```pwsh
	 # Preview changes without applying them
	 az deployment sub create `
	   --location westus2 `
	   --template-file main.bicep `
	   --parameters '@main.parameters.json' `
	   --what-if
	 ```

3. Verify the deployment in the Azure Portal or via `az group show --name <rg-name>`.

> The template (`main.bicep`) exposes `resourceGroupName`, `location`, and `tags` parameters and outputs the resulting `resourceGroupId` for chaining into downstream deployments.

## Clean Up

Delete the resource group (and all resources created inside it) when you are done:

```pwsh
az group delete `
	--name rg-simplebicep `
	--yes `
	--no-wait
```

Omit `--no-wait` if you want to block until deletion finishes, and change `rg-simplebicep` if you deployed with a different name.
