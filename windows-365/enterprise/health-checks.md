---
# required metadata
title: Azure network connection health checks in Windows 365
titleSuffix:
description: Learn about the health checks that are automatically run on Azure network connections.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/07/2022
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Azure network connections health checks

A unique feature of Windows 365 is the Azure network connection (ANC) health checks. The health checks are periodically run to make sure that

- Cloud PC provisioning is successful.
- End-user Cloud PC experiences are optimal.

## Azure network connection status

In the **Azure network connection** tab, every ANC created displays a status. This status helps you determine if new Cloud PCs can be expected to provision successfully, and that existing end-users are having an optimal Cloud PC experience.

Statuses include:

- **Running checks**: The health checks are currently running. The ANC list view automatically refreshes every five minutes. Wait for the checks to complete before attempting to assign it to a provisioning policy.
- **Checks successful**: All health checks passed. The ANC is ready for use.
- **Checks successful with warnings**: All critical health checks passed. However at least one non-critical check may have issues. An example of a check that may trigger this state is the hybrid Azure AD join sync check. Hybrid Azure AD join sync can take up to 90 minutes, so we check much of the hybrid Azure AD join sync service but can’t confirm the device sync succeeded until later. ANCs with this status can be used by provisioning policies.
- **Checks failed**: One or more required checks failed. An ANC can’t be used if it's in a failed state. You’ll have to resolve the underlying issue and Retry the health checks.

## Status error details

Every failed ANC or success with warning error state includes the technical details behind the failure. Select the **View details** link for each failed check to view more information on the failure. After you’ve fixed the underlying issue, **Retry** the health check to rerun the tests.

## Supported checks

- **DNS can resolve Active Directory domain**: Resolve the provided Active Directory domain name.
- **Active directory domain join**: A domain join using the credentials, domain, and OU provided.
- **Endpoint connectivity**: Connectivity to the required [URL/endpoints](requirements-network.md).
- **Azure AD device sync (warning)**: Azure AD sync is enabled on the Azure AD tenant, and the computer object is being synced within 90 minutes.
- **Azure subnet IP address usage**: Sufficient IP addresses are available in the provided Azure subnet.
- **Azure tenant readiness**: The defined Azure subscription is enabled and ready for use. No Azure policy restrictions are blocking Windows 365 resources from being created.
- **Azure virtual network readiness**: The defined vNet is in a Windows 365 supported region.
- **First party app permissions exist on Azure subscription**: Sufficient permissions exist on the Azure subscription.
- **First party app permissions exist on Azure resource group**: Sufficient permissions exist on the Azure resource group.
- **First party app permissions exist on Azure virtual network**: Sufficient permissions exist on the Azure vNet.
- **Environment and configuration is ready**: Underlying infrastructure is ready for provisioning to succeed.
- **Intune enrollment restrictions allow Windows enrollment**: Verify that Intune enrollment restrictions are configured to allow Windows enrollment.
- **Localization language package readiness**: Verify that the operating system and Microsoft 365 language packages are reachable. Also verify that the localization package download link is reachable.

<!-- ########################## -->
## Next steps

[Learn more about Azure network connections](azure-network-connections.md).
