---
severity: Important
pillar: Reliability
category: RE:05 Regions and availability zones
resource: Storage Account
resourceType: Microsoft.Storage/storageAccounts
online version: https://azure.github.io/PSRule.Rules.Azure/en/rules/Azure.Storage.UseReplication/
---

# Storage Account is available in a single zone

## SYNOPSIS

Storage Accounts using the LRS SKU are only replicated within a single zone.

## DESCRIPTION

Storage Accounts can be configured with several different durability options that replicate data between regions/ zones.

Azure provides a number of geo-replicated options including;
Geo-redundant storage and geo-zone-redundant storage.
Geo-zone-redundant storage is only available in supported regions.

The following geo-replicated and zone-replicated options are available within Azure:

- `Standard_GRS`
- `Standard_RAGRS`
- `Standard_GZRS`
- `Standard_RAGZRS`
- `Premium_ZRS`
- `Standard_GZRS`
- `Standard_RAGZRS`
- `Standard_ZRS`

## RECOMMENDATION

Consider using a zone-redundant or geo-replicated SKU for storage accounts that contain data.

## EXAMPLES

### Configure with Azure template

To deploy Storage Accounts that pass this rule:

- Set the `sku.name` property to a geo-replicated SKU.
  Such as `Standard_GRS`.

For example:

```json
{
  "type": "Microsoft.Storage/storageAccounts",
  "apiVersion": "2023-05-01",
  "name": "[parameters('name')]",
  "location": "[parameters('location')]",
  "sku": {
    "name": "Standard_GRS"
  },
  "kind": "StorageV2",
  "properties": {
    "allowBlobPublicAccess": false,
    "supportsHttpsTrafficOnly": true,
    "minimumTlsVersion": "TLS1_2",
    "accessTier": "Hot",
    "allowSharedKeyAccess": false,
    "networkAcls": {
      "defaultAction": "Deny"
    }
  }
}
```

### Configure with Bicep

To deploy Storage Accounts that pass this rule:

- Set the `sku.name` property to a geo-replicated SKU.
  Such as `Standard_GRS`.

For example:

```bicep
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
  name: name
  location: location
  sku: {
    name: 'Standard_GRS'
  }
  kind: 'StorageV2'
  properties: {
    allowBlobPublicAccess: false
    supportsHttpsTrafficOnly: true
    minimumTlsVersion: 'TLS1_2'
    accessTier: 'Hot'
    allowSharedKeyAccess: false
    networkAcls: {
      defaultAction: 'Deny'
    }
  }
}
```

<!-- external:avm avm/res/storage/storage-account skuName -->

## NOTES

This rule is not applicable for premium storage accounts.
Storage Accounts with the following tags are automatically excluded from this rule:

- `ms-resource-usage = 'azure-cloud-shell'` - Storage Accounts used for Cloud Shell are not intended to store data.
  This tag is applied by Azure to Cloud Shell Storage Accounts by default.
- `resource-usage = 'azure-functions'` - Storage Accounts used for Azure Functions.
  This tag can be optionally configured.
- `resource-usage = 'azure-monitor'` - Storage Accounts used by Azure Monitor are intended for diagnostic logs.
  This tag can be optionally configured.

## LINKS

- [RE:05 Regions and availability zones](https://learn.microsoft.com/azure/well-architected/reliability/regions-availability-zones)
- [Azure Storage redundancy](https://learn.microsoft.com/azure/storage/common/storage-redundancy)
- [Azure deployment reference](https://learn.microsoft.com/azure/templates/microsoft.storage/storageaccounts)
