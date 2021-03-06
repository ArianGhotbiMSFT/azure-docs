---
title: Add and remove administrative units - Azure Active Directory | Microsoft Docs
description: Use administrative units to restrict the scope of role permissions in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
ms.service: active-directory
ms.topic: how-to
ms.subservice: roles
ms.workload: identity
ms.date: 11/04/2020
ms.author: curtand
ms.reviewer: anandy
ms.custom: oldportal;it-pro;
ms.collection: M365-identity-device-management
---

# Manage administrative units in Azure Active Directory

For more granular administrative control in Azure Active Directory (Azure AD), you can assign users to an Azure AD role with a scope that's limited to one or more administrative units.

## Get started

1. To run queries from the following instructions via [Graph Explorer](https://aka.ms/ge), do the following:

    a. In the Azure portal, go to Azure AD. 
    
    b. In the applications list, select **Graph explorer**.
    
    c. On the **Permissions** pane, select **Grant admin consent for Graph explorer**.

    ![Screenshot showing the "Grant admin consent for Graph explorer" link.](./media/admin-units-manage/select-graph-explorer.png)


1. Use the preview version of Azure AD PowerShell.

## Add an administrative unit

You can add an administrative unit by using either the Azure portal or PowerShell.

### Use the Azure portal

1. In the Azure portal, go to Azure AD. Then, on the left pane, select **Administrative units**.

    ![Screenshot of the "Administrative units" link in Azure AD.](./media/admin-units-manage/nav-to-admin-units.png)

1. Select the **Add** button at the upper part of the pane, and then, in the **Name** box, enter the name of the administrative unit. Optionally, add a description of the administrative unit.

    ![Screenshot showing the Add button and the Name box for entering the name of the administrative unit.](./media/admin-units-manage/add-new-admin-unit.png)

1. Select the blue **Add** button to finalize the administrative unit.

### Use PowerShell

Install Azure AD PowerShell (preview) before you try to run the following commands:

```powershell
Connect-AzureAD
New-AzureADMSAdministrativeUnit -Description "West Coast region" -DisplayName "West Coast"
```

You can modify the values that are enclosed in quotation marks, as required.

### Use Microsoft Graph

```http
Http Request
POST /administrativeUnits
Request body
{
  "displayName": "North America Operations",
  "description": "North America Operations administration"
}
```

## Remove an administrative unit

In Azure AD, you can remove an administrative unit that you no longer need as a unit of scope for administrative roles.

### Use the Azure portal

1. In the Azure portal, go to **Azure AD**, and then select **Administrative units**. 
1. Select the administrative unit to be deleted, and then select **Delete**. 
1. To confirm that you want to delete the administrative unit, select **Yes**. The administrative unit is deleted.

![Screenshot of the administrative unit Delete button and confirmation window.](./media/admin-units-manage/select-admin-unit-to-delete.png)

### Use PowerShell

```powershell
$delau = Get-AzureADMSAdministrativeUnit -Filter "displayname eq 'DeleteMe Admin Unit'"
Remove-AzureADMSAdministrativeUnit -ObjectId $delau.ObjectId
```

You can modify the values that are enclosed in quotation marks, as required for the specific environment.

### Use the Graph API

```http
HTTP request
DELETE /administrativeUnits/{Admin id}
Request body
{}
```

## Next steps

* [Manage users in an administrative unit](admin-units-add-manage-users.md)
* [Manage groups in an administrative unit](admin-units-add-manage-groups.md)
