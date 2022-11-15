# purelyequinix

Starting this repo to track scripts used in Equinix Metal

when creating a windows instance this would go in the userdata section

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Install-PackageProvider -Name NuGet -force
Install-Module -Name PureStoragePowerShellToolkit -force

add-netlbfoTeamNIC -Team "bond_bond0" -VlanID 1009 -Confirm:$false

Set-MPIOSetting -NewPathRecoveryInterval 20 -CustomPathRecovery Enabled -NewPDORemovePeriod 30 -NewDiskTimeout 60 -NewPathVerificationState Enabled
New-MSDSMSupportedHw -VendorId PURE -ProductId FlashArray

Update-Help -Confirm:$false


Add-WindowsFeature -Name 'Multipath-IO' -restart -Confirm:$false


DHCP wip
Install-WindowsFeature DHCP -IncludeManagementTools
New-NetIPAddress -IPAddress 192.168.9.2 -InterfaceAlias "bond_bond0 - VLAN 1009" -DefaultGateway 192.168.9.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.168.9.2

Add-DhcpServerv4Scope -name "deploy" -StartRange 192.168.9.1 -EndRange 192.168.9.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 192.168.9.0 -StartRange 192.168.9.1 -EndRange 192.168.9.99
Set-DhcpServerv4OptionValue -OptionID 3 -Value 192.168.9.1 -ScopeID 192.168.9.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain pureonmetal.com -DnsServer 192.168.0.5
