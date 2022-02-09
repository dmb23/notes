# Accessing Data Sources with Synapse

When creating a Synapse Workspace from the portal, some processes are automated in the background:

- the *workspace managed identity* is given the `storageBlobDataContributor` role on the primary storage account. 
	- this allows to access the storage account via linked services / datasets (?)
- the *user* is given the `storageBlobDataContributor` role on the primary storage account
	- shouldn't they be anyways `owner`?
	- this allows to search the storage account like a file system in the data browser (?)
- If the Storage Account is secured (AKA does not accept public connections or more general is Blocked by the firewall) it is necessary to create a Managed Private Endpoint from the Managed VNet of the Synapse Workspace.

> [this page](https://docs.microsoft.com/en-gb/azure/synapse-analytics/security/connect-to-a-secure-storage-account?WT.mc_id=Portal-Microsoft_Azure_Synapse#access-a-secured-storage-account) mentions another option to safely connect, which becomes necessary if dedicated / Serverless SQL pools (which are not deployed into the managed VNet) want to access the storage account {.is-note}

Dedicated / Serverless SQL pools are not deployed into the Managed VNet.

- Therefore Managed Private Endpoints are automatically created for them.
- Therefore it may require to set the Managed Workspace Identity as a trusted Azure Service in a secured storage account - according to [this page](https://docs.microsoft.com/en-gb/azure/synapse-analytics/security/connect-to-a-secure-storage-account?WT.mc_id=Portal-Microsoft_Azure_Synapse#access-a-secured-storage-account) - instead of allowing trusted access via a Managed Private Endpoint.
