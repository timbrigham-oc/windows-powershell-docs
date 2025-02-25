---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.ConfigCI.Commands.dll-Help.xml
Module Name: ConfigCI
ms.date: 12/20/2016
online version: https://learn.microsoft.com/powershell/module/configci/new-cipolicy?view=windowsserver2016-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: New-CIPolicy
---

# New-CIPolicy

## SYNOPSIS
Creates a Code Integrity policy as an .xml file.

## SYNTAX

### Drivers
```
New-CIPolicy [-FilePath] <String> [-DriverFiles <DriverFile[]>] -Level <RuleLevel> [-Fallback <RuleLevel[]>]
 [-Audit] [-ScanPath <String>] [-ScriptFileNames] [-UserPEs] [-NoScript] [-Deny] [-NoShadowCopy]
 [-OmitPaths <String[]>] [-PathToCatroot <String>] [<CommonParameters>]
```

### Rules
```
New-CIPolicy [-FilePath] <String> -Rules <Rule[]> [-Audit] [-ScanPath <String>] [-ScriptFileNames] [-UserPEs]
 [-NoScript] [-Deny] [-NoShadowCopy] [-OmitPaths <String[]>] [-PathToCatroot <String>] [<CommonParameters>]
```

## DESCRIPTION
The **New-CIPolicy** cmdlet creates a Code Integrity policy as an .xml file.

If you specify **DriverFile** objects, this cmdlet generates rules based on the **Level** parameter.
This cmdlet creates a policy based on those rules for the specified drive files.

If you specify **Rule** objects, this cmdlet creates a policy based on those objects.
Because the rules that you specify are created at a specific level, do not specify a level.

If you do not supply either driver files or rules, this cmdlet performs a system scan similar to the **Get-SystemDriver** cmdlet.
The cmdlet generates rules based on **Level**.
If you specify the **Audit** parameter, this cmdlet scans the Code Integrity Audit log instead.

## EXAMPLES

### Example 1: Create a policy
```
The first command scans for user-mode executables (applications) along with kernel-mode binaries such as drivers and creates rules at the Publisher level. The command creates a policy and stores it in the file that is named Policy.xml. This command specifies the **OmitPaths** parameter to exclude files in the temp\ConfigCITestBinaries folder. The command specifies the **NoScript** parameter so that it gets information for only PE files.
PS C:\> New-CIPolicy -ScanPath '.\temp\' -UserPEs -OmitPaths '.\temp\ConfigCITestBinaries' -NoScript -FilePath '.\Policy.xml' -Level Publisher
Scan completed successfully

The second command displays the contents of the policy. 
PS C:\> Get-Content -Path '.\policy.xml'
<?xml version="1.0" encoding="utf-8"?>
<SiPolicy xmlns="urn:schemas-microsoft-com:sipolicy">
  <VersionEx>10.0.0.0</VersionEx>
  <PolicyTypeID>{A244370E-44C9-4C06-B551-F6016E563076}</PolicyTypeID>
  <PlatformID>{2E07F7E4-194C-4D20-B7C9-6F44A6C5A234}</PlatformID>
  <Rules>
    <Rule>
      <Option>Enabled:Unsigned System Integrity Policy</Option>
    </Rule>
    <Rule>
      <Option>Enabled:Audit Mode</Option>
    </Rule>
    <Rule>
      <Option>Enabled:Advanced Boot Options Menu</Option>
    </Rule>
    <Rule>
      <Option>Enabled:UMCI</Option>
    </Rule>
    <Rule>
      <Option>Disabled:Script Enforcement</Option>
    </Rule>
  </Rules>
  <!--EKUS-->
  <EKUs />
  <!--File Rules-->
  <FileRules>
    <Allow ID="ID_ALLOW_A_2F" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Sha1" Hash="BE0777
F5AF88628D4555A875036648DF1AD19BBE" />
    <Allow ID="ID_ALLOW_A_30" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Sha256" Hash="6FA5
AF724499C338A77FEEAD90F55DDF5F23D081C6DCE8E9DF486E95C6A9B310" />
    <Allow ID="ID_ALLOW_A_31" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Page Sha1" Hash="D
41570F2E6E7E6245CF342131D4706C944562B1E" />
    <Allow ID="ID_ALLOW_A_32" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Page Sha256" Hash=
"F714D9784E15B88F56180C8EE2B40C769CC83428954585A1DCF9A260FE967CDD" />
    <Allow ID="ID_ALLOW_A_37" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Sha1" Ha
sh="FD58E1BFA1E661C809F8A2437932B0F0308A99F8" />
    <Allow ID="ID_ALLOW_A_38" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Sha256"
Hash="A1C9FA473C2D79D0F68DF6EC72E31847F0FDA283D3A9E6B1405B0DF5929CCCB8" />
    <Allow ID="ID_ALLOW_A_39" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Page Sha
1" Hash="6D3764B75C6502634234911B8F224FC9568217C9" />
    <Allow ID="ID_ALLOW_A_3A" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Page Sha
256" Hash="2196AD3A00A59F4C35EEF7FE843FA3D6F80D5EFB3C674ADC087396B77AB35768" />
    <Allow ID="ID_ALLOW_A_3F" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Sha1" Ha
sh="28FAEFE1B18A979F9FF55744B22C6E5EA2949959" />
    <Allow ID="ID_ALLOW_A_40" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Sha256"
Hash="DA737C142A51A73D82E6AD677474C8031486FDEF018A6FE9D178564F83AB284B" />
    <Allow ID="ID_ALLOW_A_41" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Page Sha
1" Hash="029606A9B560F4921EC1122AA73C19C9B97F7764" />
    <Allow ID="ID_ALLOW_A_42" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Page Sha
256" Hash="2A5D6BCBFA55DB0F0487F45F4A6986AFC2C4783820EDA48DE9E0560E51D8DB56" />
    <Allow ID="ID_ALLOW_A_33" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Sha1" Hash="BE0777F5AF88628D4555A875036648DF1AD19BBE" />
    <Allow ID="ID_ALLOW_A_34" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Sha256" Hash="6FA5
AF724499C338A77FEEAD90F55DDF5F23D081C6DCE8E9DF486E95C6A9B310" />
    <Allow ID="ID_ALLOW_A_35" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Page Sha1" Hash="D
41570F2E6E7E6245CF342131D4706C944562B1E" />
    <Allow ID="ID_ALLOW_A_36" FriendlyName="\\?\E:\cmdlets\temp\Microsoft.ConfigCI.Commands.dll Hash Page Sha256" Hash=
"F714D9784E15B88F56180C8EE2B40C769CC83428954585A1DCF9A260FE967CDD" />
    <Allow ID="ID_ALLOW_A_3B" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Sha1" Hash="FD58E1BFA1E661C809F8A2437932B0F0308A99F8" />
    <Allow ID="ID_ALLOW_A_3C" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Sha256"
Hash="A1C9FA473C2D79D0F68DF6EC72E31847F0FDA283D3A9E6B1405B0DF5929CCCB8" />
    <Allow ID="ID_ALLOW_A_3D" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Page Sha
1" Hash="6D3764B75C6502634234911B8F224FC9568217C9" />
    <Allow ID="ID_ALLOW_A_3E" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\ntoskrnl.exe Hash Page Sha
256" Hash="2196AD3A00A59F4C35EEF7FE843FA3D6F80D5EFB3C674ADC087396B77AB35768" />
    <Allow ID="ID_ALLOW_A_43" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Sha1" Ha
sh="28FAEFE1B18A979F9FF55744B22C6E5EA2949959" />
    <Allow ID="ID_ALLOW_A_44" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Sha256"
Hash="DA737C142A51A73D82E6AD677474C8031486FDEF018A6FE9D178564F83AB284B" />
    <Allow ID="ID_ALLOW_A_45" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Page Sha
1" Hash="029606A9B560F4921EC1122AA73C19C9B97F7764" />
    <Allow ID="ID_ALLOW_A_46" FriendlyName="\\?\E:\cmdlets\temp\PackageInspectorTestBinaries\storahci.sys Hash Page Sha
256" Hash="2A5D6BCBFA55DB0F0487F45F4A6986AFC2C4783820EDA48DE9E0560E51D8DB56" />
  </FileRules>
  <!--Signers-->
  <Signers>
    <Signer ID="ID_SIGNER_S_D" Name="MSIT Test CodeSign CA 3">
      <CertRoot Type="TBS" Value="FA6B9A2230CE08BCA81D096B28CF495672401D3A43A0D285CF352464A6C9C7FD" />
      <CertPublisher Value="Microsoft Windows" />
    </Signer>
    <Signer ID="ID_SIGNER_S_E" Name="MSIT Test CodeSign CA 3">
      <CertRoot Type="TBS" Value="FA6B9A2230CE08BCA81D096B28CF495672401D3A43A0D285CF352464A6C9C7FD" />
      <CertPublisher Value="Microsoft Windows" />
    </Signer>
    <Signer ID="ID_SIGNER_S_13" Name="VeriSign Class 3 Code Signing 2010 CA">
      <CertRoot Type="TBS" Value="4843A82ED3B1F2BFBEE9671960E1940C942F688D" />
      <CertPublisher Value="NVIDIA Corporation" />
    </Signer>
    <Signer ID="ID_SIGNER_S_14" Name="Microsoft Windows Third Party Component CA 2012">
      <CertRoot Type="TBS" Value="CEC1AFD0E310C55C1DCC601AB8E172917706AA32FB5EAF826813547FDF02DD46" />
      <CertPublisher Value="Microsoft Windows Hardware Compatibility Publisher" />
    </Signer>
    <Signer ID="ID_SIGNER_S_15" Name="VeriSign Class 3 Code Signing 2010 CA">
      <CertRoot Type="TBS" Value="4843A82ED3B1F2BFBEE9671960E1940C942F688D" />
      <CertPublisher Value="NVIDIA Corporation" />
    </Signer>
    <Signer ID="ID_SIGNER_S_16" Name="Microsoft Windows Third Party Component CA 2012">
      <CertRoot Type="TBS" Value="CEC1AFD0E310C55C1DCC601AB8E172917706AA32FB5EAF826813547FDF02DD46" />
      <CertPublisher Value="Microsoft Windows Hardware Compatibility Publisher" />
    </Signer>
  </Signers>
  <!--Driver Signing Scenarios-->
  <SigningScenarios>
    <SigningScenario Value="131" ID="ID_SIGNINGSCENARIO_DRIVERS_1" FriendlyName="Auto generated policy on 11-13-2015">
      <ProductSigners>
        <FileRulesRef>
          <FileRuleRef RuleID="ID_ALLOW_A_2F" />
          <FileRuleRef RuleID="ID_ALLOW_A_30" />
          <FileRuleRef RuleID="ID_ALLOW_A_31" />
          <FileRuleRef RuleID="ID_ALLOW_A_32" />
          <FileRuleRef RuleID="ID_ALLOW_A_37" />
          <FileRuleRef RuleID="ID_ALLOW_A_38" />
          <FileRuleRef RuleID="ID_ALLOW_A_39" />
          <FileRuleRef RuleID="ID_ALLOW_A_3A" />
          <FileRuleRef RuleID="ID_ALLOW_A_3F" />
          <FileRuleRef RuleID="ID_ALLOW_A_40" />
          <FileRuleRef RuleID="ID_ALLOW_A_41" />
          <FileRuleRef RuleID="ID_ALLOW_A_42" />
        </FileRulesRef>
        <AllowedSigners>
          <AllowedSigner SignerId="ID_SIGNER_S_D" />
          <AllowedSigner SignerId="ID_SIGNER_S_13" />
          <AllowedSigner SignerId="ID_SIGNER_S_14" />
        </AllowedSigners>
      </ProductSigners>
    </SigningScenario>
    <SigningScenario Value="12" ID="ID_SIGNINGSCENARIO_WINDOWS" FriendlyName="Auto generated policy on 11-13-2015">
      <ProductSigners>
        <FileRulesRef>
          <FileRuleRef RuleID="ID_ALLOW_A_33" />
          <FileRuleRef RuleID="ID_ALLOW_A_34" />
          <FileRuleRef RuleID="ID_ALLOW_A_35" />
          <FileRuleRef RuleID="ID_ALLOW_A_36" />
          <FileRuleRef RuleID="ID_ALLOW_A_3B" />
          <FileRuleRef RuleID="ID_ALLOW_A_3C" />
          <FileRuleRef RuleID="ID_ALLOW_A_3D" />
          <FileRuleRef RuleID="ID_ALLOW_A_3E" />
          <FileRuleRef RuleID="ID_ALLOW_A_43" />
          <FileRuleRef RuleID="ID_ALLOW_A_44" />
          <FileRuleRef RuleID="ID_ALLOW_A_45" />
          <FileRuleRef RuleID="ID_ALLOW_A_46" />
        </FileRulesRef>
        <AllowedSigners>
          <AllowedSigner SignerId="ID_SIGNER_S_E" />
          <AllowedSigner SignerId="ID_SIGNER_S_15" />
          <AllowedSigner SignerId="ID_SIGNER_S_16" />
        </AllowedSigners>
      </ProductSigners>
    </SigningScenario>
  </SigningScenarios>
  <UpdatePolicySigners />
  <CiSigners>
    <CiSigner SignerId="ID_SIGNER_S_E" />
    <CiSigner SignerId="ID_SIGNER_S_15" />
    <CiSigner SignerId="ID_SIGNER_S_16" />
  </CiSigners>
  <HvciOptions>0</HvciOptions>
</SiPolicy>
```

### Example 2: Scan unsigned files
```
PS C:\> New-CIPolicy -ScanPath '.\temp\' -UserPEs -FilePath ".\policy.xml" -Level Publisher -Fallback Hash
Unable to generate rules for all scanned files at the requested level.  A list 
of files not covered by the current policy can be found at 
C:\Users\tocal\AppData\Local\Temp\tmp2F2D.tmp.  If it is safe to not include 
these files, no action needs to be taken, otherwise a more complete policy may 
be created using the -fallback switch
```

This command scans for user-mode executables (applications) along with kernel-mode binaries such as drivers, and then creates rules at the Publisher level, just as the first example did.
This command does not specify the **OmitPaths** and **NoScript** parameters.
The command encounters files that have an invalid or corrupted signature format.
The cmdlet returns an informational message about generated rules.

### Example 3: Create rules for driver files in a variable
```
PS C:\> $DriverFiles = Get-SystemDriver -ScanPath '.\temp\' -UserPEs -OmitPaths '.\temp\ConfigCITestBinaries' -NoScript
PS C:\> New-CIPolicy -Level Publisher -Fallback Hash -FilePath '.\policy02.xml' -DriverFiles $DriverFiles
```

The first command gets drivers by using the **Get-SystemDriver** cmdlet, and then stores them in the $DriverFiles variable.

The second command creates rules at the Publisher level for the items stored in $DriverFiles.
This example has the same effect as the single command in the second example.

## PARAMETERS

### -Audit
Indicates that this cmdlet searches the Code Integrity Audit log for drivers.
It does not perform a full system scan.
Specify this parameter only if you do not provide driver files or rules.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: a

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Deny
Indicates that this cmdlet creates deny rules instead of the default allow rules.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: d

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DriverFiles
Specifies an array of **DriverFile** objects on which this cmdlet bases rules.
To obtain a driver file, use the **Get-SystemDriver** cmdlet.

```yaml
Type: DriverFile[]
Parameter Sets: Drivers
Aliases: df

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Fallback
Specifies an array of levels of detail for generated rules.
If this cmdlet cannot generate a rule at the specified level, this cmdlet attempts to generate it at a fallback level.
The acceptable values for this parameter are the same as for **Level**.
If you specify multiple fallback levels, this cmdlet tries them in order.

```yaml
Type: RuleLevel[]
Parameter Sets: Drivers
Aliases: 
Accepted values: None, Hash, FileName, FilePath, SignedVersion, PFN, Publisher, FilePublisher, LeafCertificate, PcaCertificate, RootCertificate, WHQL, WHQLPublisher, WHQLFilePublisher

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilePath
Specifies the path for the Code Integrity policy .xml file.

```yaml
Type: String
Parameter Sets: (All)
Aliases: f

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Level
Specifies the primary level of detail for generated rules. Refer to [WDAC File Rule Levels](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-file-rule-levels) for acceptable parameter values and descriptions.

```yaml
Type: RuleLevel
Parameter Sets: Drivers
Aliases: l
Accepted values: None, Hash, FileName, FilePath, SignedVersion, PFN, Publisher, FilePublisher, LeafCertificate, PcaCertificate, RootCertificate, WHQL, WHQLPublisher, WHQLFilePublisher

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoScript
Indicates that this cmdlet does not search script files.
It searches portable executable files (PE files) only.
Specify this parameter only if you do not provide driver files or rules.

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

### -NoShadowCopy
Indicates that the Volume Snapshot Service (VSS) does not make a shadow copy of the disk while the scan runs.
This parameter could cause an incomplete scan for a system that is running.

If a scan fails due to VSS errors caused by low disk space on the target drive, this cmdlet prompts you to specify this parameter.

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

### -OmitPaths
Specifies an array of paths that this cmdlet omits from the search.
Specify this parameter only if you do not provide driver files or rules.
We recommend that you omit C:\Windows.old.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: o

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PathToCatroot
Specifies the path of the CatRoot folder.
Specify this parameter to scan a remote or mounted drive.
Specify this parameter only if you do not provide driver files or rules.

```yaml
Type: String
Parameter Sets: (All)
Aliases: c

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Rules
Specifies an array of **Rule** objects that this cmdlet includes in the policy.
To obtain a rule object, use the **Get-CIPolicy** or **New-CIPolicyRule** cmdlets.

```yaml
Type: Rule[]
Parameter Sets: Rules
Aliases: r

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ScanPath
Specifies the path for this cmdlet to scan.
You can specify a local or remote path.
Specify this parameter only if you do not provide driver files or rules.
If you specify a remote or mounted drive, also specify the **PathToCatroot** parameter.

```yaml
Type: String
Parameter Sets: (All)
Aliases: s

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ScriptFileNames
This parameter is reserved for internal Microsoft use.

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

### -UserPEs
Indicates that this cmdlet includes user-mode files in the scan.
Specify this parameter only if you do not provide driver files or rules.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: u

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

Policy objects created by New-CIPolicyRule with level of 'Publisher' may fail to create a CI Policy XML. The 'Root' attribute must be set to a real TBS signature, not the literal value 'Unknown'. This will result in the rule will be silently dropped, and not imported by New-CiPolicy. This can pose an issue as the Fallback paramater used by New-CIPolicyRule or internally by New-CIPolicy is not properly triggered, resulting in incomplete rules. 

Example content that will be silently skipped: 

```
PS C:\> $DriverFiles = Get-SystemDriver -ScanPath "C:\Example" -UserPEs
PS C:\> $Rules = New-CIPolicyRule -Level Publisher -DriverFiles $DriverFiles 
"Scan completed successfully"
PS C:\> $Rules

Name           : Example Certificate Root
Id             : ID_SIGNER_xx_xxx
TypeId         : Allow
Root           : Unsupported
FileVersionRef :
AppIDRef       :
Wellknown      : False
Ekus           :
Exceptions     :
FileAttributes :
FileException  : False
UserMode       : True
attributes     : {[CertPublisher, Example Certificate Holder]}

PS C:> New-CIPolicy -FilePath .\Example.xml -Rules $Rules -Verbose

```


## RELATED LINKS

[Get-CIPolicy](./Get-CIPolicy.md)

[Get-SystemDriver](./Get-SystemDriver.md)

[Merge-CIPolicy](./Merge-CIPolicy.md)

[New-CIPolicyRule](./New-CIPolicyRule.md)
