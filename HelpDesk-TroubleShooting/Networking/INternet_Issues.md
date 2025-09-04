# Internet Connection TroubleShooting (Windows)

## Symptoms

- User reports no internet access.
- Other devices may/may not be affected.

## Step 1 - Check physical and adapter status

```powershell
Get-NetAdapter | Format-Table Name, Status, LinkSpeed
Get-NetIPConfiguration
# Look for "Disconnected" or "Disabled"
# If no IPv4 or Gateway look to DHCP
```

## Step 2 - Test Gateway

```powershell
$gw = (Get-NetIPConfiguration | Where-Object {$_.IPv4DefaultGateway}).IPv4DefaultGateway.NextHop
Test-NetConnection $gw -InformationLevel Detailed
# If failure here look at local NIC/switch/cables/wifiAP problems
```

## Step 3 - Test to reach WAN

```powershell
Test-NetConnection 8.8.8.8 -Informationlevel Detailed
# If 8.8.8.8 is reached, but internet is still broken look to DNS proxy issues
```

## Step 4 - Do a Router check 

```powershell
Get-NetRoute -DestinationPrefix "0.0.0.0/0" | Sort-Object -Property RouteMetric | Format-Table ifIndex,NextHop,RouteMetric
# If 'no default route or nexthop' look at renewing DHCP
```

## Step 5 - DNS checks

```powershell
# Who are we using
Get-DnsClientServerAddress | Where-Object {$_.AddressFamily -eq 2} | Format-Table InterfaceAlias, ServerAddresses

# Can we resolve and connect to HTTPS
Resolve-DnsName microsoft.com
Test-NetConnection microsoft.com -Port 443 -InformationLevel Quiet

# If resolves fail look at fixing DNS or flush and renew below
# Resolves OK, but 443 fails look at proxy, firewall, or upstream block
```

## Step 6 - Proxy/VPN checks

```powershell
# WinHTTP proxy (affects may system services)
netsh winhttp show proxy

# User proxy (browser/WinINET)
Get-ItemProperty 'HKCU:\Software\Microsoft\Window\CurrentVersion\Internet Settings'
| Select-Object ProxyEnable,ProxyServer,AutoconfigURL

# VPNs that might be forcing bad routes/DNS
Get-VpnConnection

# If proxy is set but should not be: disable it or fix URL
# Disconnect stale VPNs and retest
```

## Step 7 - Firewall/profile checks

```powershell
Get-NetFirewallProfile | Format-Table Name, Enabled,DefaultInboundAction,DefaultOutboundAction

# If outbound = block(without rules) will nuke web, flip to test
```

## Step 8 - Wifi checks

```powershell
netsh wlan show interfaces
netsh wlan show profiles
# if the profile is corrupted, forget and re-add:
netsh wlan delete profile name="SSID"
```

## Step 9 - Reset/refresh the stack

```powershell
clear-DnsClientCache
ipconfig /release
ipconfig /renew

# Bounce the adapter (replace with you NIC name)
$nic = (Get-NetAdapter | Where-Object Status -eq 'Up').Name
Disable-NetAdapter -Name $nic -Confirm:$false: Start-Sleep 2; Enable-NetAdapter -Name $nic

# Winsock + IP reset (requires reboot after)
netsh winsock reset
netsh int ip reset
```

## Service that should stay healthy

```powershell
# DHCP client, DNS client, NLA
'DHCP','DNScache','NlaSvc' | ForEach-Object {Get-Service $_ | Select-Object Name,Status,Startype }
# If stopped:
'Dhcp','Dnscache','NlaSvc' | ForEach-Object {Start-Service $_ }
```


