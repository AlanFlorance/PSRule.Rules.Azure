---
severity: Important
pillar: Reliability
category: RE:04 Target metrics
resource: Virtual Machine
resourceType: Microsoft.Compute/virtualMachines
online version: https://azure.github.io/PSRule.Rules.Azure/en/rules/Azure.VM.BasicSku/
ms-content-id: 49cef14e-19f0-4a54-be14-7c27a0347b4c
---

# Avoid Basic VM SKU

## SYNOPSIS

Virtual machines (VMs) should not use Basic sizes.

## DESCRIPTION

VMs can be deployed in Basic or Standard sizes.
Basic VM sizes are suitable only for entry level development scenarios.

## RECOMMENDATION

Basic VM sizes are not suitable for production workloads or intensive development workloads.
Consider migration to an alternative Standard VM size.

## LINKS

- [RE:04 Target metrics](https://learn.microsoft.com/azure/well-architected/reliability/metrics)
- [Sizes for Windows virtual machines in Azure](https://learn.microsoft.com/azure/virtual-machines/windows/sizes)
- [Sizes for Linux virtual machines in Azure](https://learn.microsoft.com/azure/virtual-machines/linux/sizes)
