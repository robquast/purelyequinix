# purelyequinix

Starting this repo to track scripts used in Equinix Metal

when creating a windows instance this would go in the userdata section

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Install-PackageProvider -Name NuGet -force
Install-Module -Name PureStoragePowerShellToolkit -force

add-netlbfoTeamNIC -Team "bond_bond0" -VlanID 999 -Confirm:$false

Set-MPIOSetting -NewPathRecoveryInterval 20 -CustomPathRecovery Enabled -NewPDORemovePeriod 30 -NewDiskTimeout 60 -NewPathVerificationState Enabled
New-MSDSMSupportedHw -VendorId PURE -ProductId FlashArray

Update-Help -Confirm:$false


Add-WindowsFeature -Name 'Multipath-IO' -restart -Confirm:$false
