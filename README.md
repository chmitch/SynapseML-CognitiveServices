# SynapseML-CognitiveServices
This repo illustrates some basic examples of operationalizing cognitive services in Synapse with SynapseML


## Environment Setup

In order to recreate this demo there are several dependencies that must first be configured.  This serves as a step by step set of instructions for configuring your environment for leveraging the provided sample notebooks.


### Provision the Synapse workspace

The first thing that must be done is creation of your Synapse workspace including an attached storage account.

1. In the Azure Portal, choose "Create a Resource" and use "Synaspe" as the search criteria.
1. Choose "Azure Synapse Analytics" and click "Create"
    ![Provision Synapse](/images/synapse/01-provision-synapse.png)
1. Fill in the basics for the Synapse Workspace including, resource group, name, region and storage account, and click "Review + Create"
(Note:  It's a good idea to create a new storage account on this screen so the necessary storage roles will be automatically asssigned for you)
    ![Provision Synapse](/images/synapse/02-provision-synapse.png)
1. On the summary screen, click "Create"

### Provision Key Vault

Now that we have a Synapse Workspace we need to provision a Key Vault for storing secrets.

1. In the resoruce group you cretaed for your synapse workspace click "Create" to add a resource.
    ![Provision Key Vault](/images/keyvault/01-provision-keyvault.png)
1. Use "key vault" as the search criteria, choose the Key Vault resource and click "Create".
    ![Provision Key Vault](/images/keyvault/02-provision-keyvault.png)
1. Give the Key Vault a name, and ensure it is in the same region as your Synapse workspace.
1. Click "Review + Create" and then "Create".

### Configure Role Based Security on Key Vault

We must grant the Synapse managed identity access to Key Vault so it can read secrets at runtime.

1. Once the Key Vault finishes provisioning, click "Go to resource".
1. On the Key Vault main screen select "Access configuration".
    ![Configure Key Vault](/images/access/01-keyvault-access.png)
1. Accept the default permission model of "Valut access policy" and click "Go to access policies"
    ![Configure Key Vault](/images/access/02-keyvault-access.png)
1. Click Create to enter the access policy dialogue.
1. Choose "Get" and "List" for Secret Permissions and click "Next"
    ![Configure Key Vault](/images/access/03-keyvault-access.png)
1. Enter the name of your Synaspe Workspace as a search term, pick the resource that aligns to your workspace name, and click "Next".
    ![Configure Key Vault](/images/access/04-keyvault-access.png)
1. Click "Next", then on the final screen click "Create".

### Provision Cognitive Services

Now that we have a Synapse Workspace we need a Cognitve Services endpoint to call for text analytics.

1. In the resoruce group you cretaed for your synapse workspace click "Create" to add a resource.
    ![Provision Cognitive Services](/images/cognitive/01-provision-cognitive.png)
1. Use "key vault" as the search criteria, choose the Key Vault resource and click "Create".
    ![Provision Cognitive Services](/images/cognitive/02-provision-cognitive.png)
1. Give the Cognitive Services resource a name and click "Review + Create"
    ![Provision Cognitive Services](/images/cognitive/03-provision-cognitive.png)

### Add Cognitive Services secret to Key Vault

Now that the Cognitive Serivces endpoint is configured we need to secure the key for the endpoint in Key Vault so Synapse can read the secret at runtime.

1. Navigate to the created Cognitive Services resource.
1. Select "Keys and Endpoint", and copy the KEY 1 value.
    ![Configure Secrets](/images/secrets/01-configure-secrets.png)
1. Navigate to the Key Vault resource, and select "Secrets".
    ![Configure Secrets](/images/secrets/02-configure-secrets.png)
1. Click "Generate/Import".
1. On the Create a secret screen, give the secret a meaningful name, and past the copied value from Key 1 of the cognitive endpoint into the "secret value" field.
    ![Configure Secrets](/images/secrets/03-configure-secrets.png)
1. Click "Create"