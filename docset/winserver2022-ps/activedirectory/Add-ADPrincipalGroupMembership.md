---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.ActiveDirectory.Management.dll-Help.xml
Module Name: ActiveDirectory
ms.date: 12/27/2016
online version: https://learn.microsoft.com/powershell/module/activedirectory/add-adprincipalgroupmembership?view=windowsserver2022-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: Add-ADPrincipalGroupMembership
---

# Add-ADPrincipalGroupMembership

## SYNOPSIS
Adds a member to one or more Active Directory groups.

## SYNTAX

```
Add-ADPrincipalGroupMembership [-WhatIf] [-Confirm] [-AuthType <ADAuthType>] [-Credential <PSCredential>]
 [-Identity] <ADPrincipal> [-MemberOf] <ADGroup[]> [-Partition <String>] [-PassThru] [-Server <String>]
 [<CommonParameters>]
```

## DESCRIPTION
The **Add-ADPrincipalGroupMembership** cmdlet adds a user, group, service account, or computer as a new member to one or more Active Directory groups.

The *Identity* parameter specifies the new user, computer, or group to add.
You can identify the user, group, or computer by its distinguished name, GUID, security identifier (SID), or Security Account Manager (SAM) account name.
You can also specify a user, group, or computer object variable, such as `$<localGroupObject>`, or pass an object through the pipeline to the *Identity* parameter.
For example, you can use the **Get-ADGroup** cmdlet to get a group object and then pass the object through the pipeline to the **Add-ADPrincipalGroupMembership** cmdlet.
Similarly, you can use **Get-ADUser** or **Get-ADComputer** to get user and computer objects to pass through the pipeline.

This cmdlet collects all of the user, computer and group objects from the pipeline, and then adds these objects to the specified group by using one Active Directory operation.

The *MemberOf* parameter specifies the groups that receive the new member.
You can identify a group by its distinguished name, GUID, SID, or SAM account name.
You can also specify group object variable, such as `$<localGroupObject>`.
To specify more than one group, use a comma-separated list.
You cannot pass group objects through the pipeline to the *MemberOf* parameter.
To add to a group by passing the group through the pipeline, use the **Add-ADGroupMember** cmdlet.

For Active Directory Lightweight Directory Services (AD LDS) environments, the *Partition* parameter must be specified except in the following two conditions:

- The cmdlet is run from an Active Directory provider drive. 
- A default naming context or partition is defined for the AD LDS environment.
To specify a default naming context for an AD LDS environment, set the **msDS-defaultNamingContext** property of the Active Directory directory service agent object (nTDSDSA) for the AD LDS instance.

## EXAMPLES

### Example 1: Add a member to a group
```
PS C:\> Add-ADPrincipalGroupMembership -Identity SQLAdmin1 -MemberOf DlgtdAdminsPSOGroup
```

This command adds the user with SAM account name SQLAdmin1 to the group DlgtdAdminsPSOGroup.

### Example 2: Add filtered users to a group
```
PS C:\> Get-ADUser -Filter 'Name -like "*SvcAccount*"' | Add-ADPrincipalGroupMembership -MemberOf SvcAccPSOGroup
```

This command gets all users with SvcAccount in their name and adds it to the group SvcAccPSOGroup.

### Example 3: Add a member to a group without specifying parameters
```
PS C:\> Add-ADPrincipalGroupMembership
cmdlet Add-ADPrincipalGroupMembership at command pipeline position 1
Supply values for the following parameters: 
Identity: DavidChew
MemberOf[0]: RodcAdmins
MemberOf[1]: Allowed RODC Password Replication Group
MemberOf[2]:
```

This command demonstrates the default behavior of this cmdlet, with no parameters specified.

### Example 4: Add filtered users to a distinguished name group
```
PS C:\> Get-ADUser -Server localhost:60000 -SearchBase "DC=AppNC" -Filter "Title -eq 'Account Lead' -and Office -eq 'Branch1'" | Add-ADPrincipalGroupMembership -MemberOf "CN=AccountLeads,OU=AccountDeptOU,DC=AppNC"
```

This command adds all employees in Branch1 in the AD LDS instance localhost:60000 whose title is Account Lead to the group with the distinguished name CN=AccountLeads,OU=AccountDeptOU,DC=AppNC.

## PARAMETERS

### -AuthType
Specifies the authentication method to use.
The acceptable values for this parameter are:

- Negotiate or 0
- Basic or 1

The default authentication method is Negotiate.

A Secure Sockets Layer (SSL) connection is required for the Basic authentication method.

The following example shows how to set this parameter to Basic.

`-AuthType Basic`

```yaml
Type: ADAuthType
Parameter Sets: (All)
Aliases: 
Accepted values: Negotiate, Basic

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies the user account credentials to use to perform this task.
The default credentials are the credentials of the currently logged on user unless the cmdlet is run from an Active Directory PowerShell provider drive.
If the cmdlet is run from such a provider drive, the account associated with the drive is the default.

To specify this parameter, you can type a user name, such as User1 or Domain01\User01 or you can specify a **PSCredential** object.
If you specify a user name for this parameter, the cmdlet prompts for a password.

You can also create a **PSCredential** object by using a script or by using the **Get-Credential** cmdlet.
You can then set the *Credential* parameter to the **PSCredential** object.

If the acting credentials do not have directory-level permission to perform the task, Active Directory PowerShell returns a terminating error.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
Specifies an Active Directory principal object by providing one of the following property values.
The identifier in parentheses is the LDAP display name for the attribute.
The acceptable values for this parameter are:

- Distinguished name
- GUID (objectGUID) 
- Security identifier (objectSid) 
- A SAM account name (sAMAccountName)

The cmdlet searches the default naming context or partition to find the object.
If two or more objects are found, the cmdlet returns a non-terminating error.

This parameter can also get this object through the pipeline or you can set this parameter to an object instance.

Derived types, such as the following are also accepted:

- **Microsoft.ActiveDirectory.Management.ADGroup**
- **Microsoft.ActiveDirectory.Management.ADUser**
- **Microsoft.ActiveDirectory.Management.ADComputer**
- **Microsoft.ActiveDirectory.Management.ADServiceAccount**

This example shows how to set the parameter to a distinguished name.

`-Identity  "CN=saradavis,CN=Users,DC=corp,DC=contoso,DC=com"`

This example shows how to set this parameter to a principal object instance named principalInstance.

`-Identity $principalInstance`

```yaml
Type: ADPrincipal
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -MemberOf
Specifies the Active Directory groups to add a user, computer, or group to as a member.
You can identify a group by providing one of the following values.
Note: The identifier in parentheses is the LDAP display name for the attribute.
The acceptable values for this parameter are:

- Distinguished name
- GUID (objectGUID) 
- Security identifier (objectSid) 
- Security Account Manager (SAM) account name (sAMAccountName)

If you are specifying more than one group, use commas to separate the groups in the list.

The following example shows how to specify this parameter by using SAM account name values.

`-MemberOf "SaraDavisGroup", "JohnSmithGroup"`

```yaml
Type: ADGroup[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Partition
Specifies the distinguished name of an Active Directory partition.
The distinguished name must be one of the naming contexts on the current directory server.
The cmdlet searches this partition to find the object defined by the *Identity* parameter.

In many cases, a default value is used for the *Partition* parameter if no value is specified.
The rules for determining the default value are given below.
Note that rules listed first are evaluated first and once a default value can be determined, no further rules are evaluated.

In Active Directory Domain Services (AD DS) environments, a default value for *Partition* is set in the following cases: 

- If the *Identity* parameter is set to a distinguished name, the default value of *Partition* is automatically generated from this distinguished name.
- If running cmdlets from an Active Directory provider drive, the default value of *Partition* is automatically generated from the current path in the drive. 
- If none of the previous cases apply, the default value of *Partition* is set to the default partition or naming context of the target domain.

In Active Directory Lightweight Directory Services (AD LDS) environments, a default value for *Partition* is set in the following cases:

- If the *Identity* parameter is set to a distinguished name, the default value of *Partition* is automatically generated from this distinguished name. 
- If running cmdlets from an Active Directory provider drive, the default value of *Partition* is automatically generated from the current path in the drive. 
- If the target AD LDS instance has a default naming context, the default value of *Partition* is set to the default naming context.
To specify a default naming context for an AD LDS environment, set the **msDS-defaultNamingContext** property of the Active Directory directory service agent object (**nTDSDSA**) for the AD LDS instance. 
- If none of the previous cases apply, the *Partition* parameter does not take any default value.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru
Returns an object representing the item with which you are working.
By default, this cmdlet does not generate any output.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Server
Specifies the AD DS instance to connect to, by providing one of the following values for a corresponding domain name or directory server.
The service may be any of the following: AD LDS, AD DS, or Active Directory snapshot instance.

Specify the AD DS instance in one of the following ways:  

Domain name values:

- Fully qualified domain name
- NetBIOS name

Directory server values:  

- Fully qualified directory server name
- NetBIOS name
- Fully qualified directory server name and port

The default value for this parameter is determined by one of the following methods in the order that they are listed:

- By using the **Server** value from objects passed through the pipeline
- By using the server information associated with the AD DS Windows PowerShell provider drive, when the cmdlet runs in that drive
- By using the domain of the computer running Windows PowerShell

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.ActiveDirectory.Management.ADPrincipal
A principal object (Microsoft.ActiveDirectory.Management.ADPrincipal) that represents a user, computer or group is received by the Identity parameter.
Derived types, such as the following are also received by this parameter.

Microsoft.ActiveDirectory.Management.ADUser

Microsoft.ActiveDirectory.Management.ADComputer

Microsoft.ActiveDirectory.Management.ADServiceAccount

Microsoft.ActiveDirectory.Management.ADGroup

## OUTPUTS

### None or Microsoft.ActiveDirectory.Management.ADPrincipal
Returns a principal object that represents the modified user, computer or group object when the *PassThru* parameter is specified.
By default, this cmdlet does not generate any output.

## NOTES
* This cmdlet does not work with a read-only domain controller.
* This cmdlet does not work with an Active Directory snapshot.

## RELATED LINKS

[Add-ADGroupMember](./Add-ADGroupMember.md)

[Get-ADComputer](./Get-ADComputer.md)

[Get-ADGroup](./Get-ADGroup.md)

[Get-ADGroupMember](./Get-ADGroupMember.md)

[Get-ADPrincipalGroupMembership](./Get-ADPrincipalGroupMembership.md)

[Get-ADUser](./Get-ADUser.md)

[Remove-ADGroupMember](./Remove-ADGroupMember.md)

[Remove-ADPrincipalGroupMembership](./Remove-ADPrincipalGroupMembership.md)

