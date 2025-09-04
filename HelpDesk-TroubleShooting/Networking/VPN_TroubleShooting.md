# VPN Troubleshooting Playbook

## Symptom - User cannot connect at all

# Step one - Basic First-Line Verification

- confirm VPN client is installed and updated
- check users credentials (password, MFA tokens)
- verify internet access without VPN
- if on wifi, confirm not on a captive portal

# Step two

## Ping Gateway

```powershell
Test-NetConnection 8.8.8.8
```

## DNS Resolution

```powershell
Resolve-DnsName vpn.company.com

# If DNS fails, set alternate DNS (8.8.8.8/1.1.1.1) and retry.
```

# Step Three

## Identify VPN Type and Ports

### VPNs use different ports and protocols. Make sure the any of the following are not blocked by firewall, ISP, or router

- IPSec (IKEv2/L2TP): UDP 500, UDP 4500, ESP ( IP protocol 50 )

- SSL VPN ( OpenVPN/AnyConnect): TCP/UDP 443 ( sometimes 1194 )

- Wireguard: UDP 51820

# Step Four

## Verify Local Firewall Status

```powershell
# Check Windows Firewall profiles
Get-NetFirewallProfiles | Format-Table Name, Enabled, DefaultOutboundAction
```

## Ensure outboundis not set to Block by default

```powershell
# Confirm VPN services are running
Get-Service RasMan
```

# Step Five

## Authentication and Certificates

## Symptoms - VPN connects, then drops immediately

- Check certificate validity ( mmc.exe -> Certificate snap-in )
- Confirm the client's time/date is correct ( certs fail if clock is off )
- For MFA: make sure push/SMS/token is working

# Step Six

## Routing and Split tunneling issues

## Symptoms: VPN connects, but user can not reach company resources

```powershell
Get-NetRoute -DestinationPrefix "0.0.0.0/0"
# Conflicting default routes -> may need split-tunneling enabled
# Try pinging an internal by IP. If that works, DNS over VPN is failing
```

# Step Seven

## Symptom: VPN Connects, IP works but hostname does not

```powershell
# Check DNS suffixes assigned by VPN
Get-DnsClientServerAddress

# Flush caches
Clear-DnsClientCache

# If DNS is not updating, force re-register
ipconfig /registerdns
```

# Step Eight

## Check Logs and EventViewer

### Window logs

- EventViewer -> Application and Service Logs -> Microsoft -> Windows -> Rasclient

### VPN Client Logs

- Many VPN apps ( AnyConnect, FortiClient, GlobalProtect ) have built-in log windows or export function

# Step Nine

## Avanced Escalation

- Test from a different network ( home vs. office vs. hotspot )
- Try reinstalling VPN client with admin rights
- Collect logs and escalate to networking/security team if the issue looks server-side

# Step Ten

## Quick Fix Commands

```powershell
# Reset IP stack
netsh int ip reset
netsh winsock reset

# Release and renew IP
ipconfig /release
ipconfig /renew

# Flush DNS
ipconfig /flushdns
```




