# Printer TroubleShooting Playbook

# Printer will not power on

## Symptoms - No lights, No display, will not respond

## TroubleShooting Steps

- Verify power cable is plugged in secured 
- Check the surge protector/UPS outlet
- If still dead -> eacalate

# Printer is offline/Not responding

## Symptoms - User sees "Printer offline" in Windows and/or jobs stuck in queue

## TroubleShooting Steps

- Restart the printer
- Check the network connection ( WiFi or Ethernet cable )
- Ping the printers IP

```powershell
Test-Connection <printer_IP>
```

- Verify the printer is set as default in Windows
- Clear the queue

```powershell
net stop spooler
del %systemroot%\System32\spool\PRINTER\* /Q
net start spooler
```

# Cannot Print to Network Printer

## Symptoms - Printer reachable, but jobs will not print

## TroubleShooting Steps

- Confirm the user has access permissions to the orinter
- Re-add printer
    `\\ServerName\PrinterShare` or Add Printer Wizard
- Verify correct drivers are installed
- Check print server for errors or spooler service issues

# Slow Printing or Delayed Jobs

## Symptoms: Jobs take minutes to start

## TroubleShooting Steps

- Check printer memory/queue - too many jobs bavked up
- Restart Printer Service

```powershell
net stop spooler && net start spooler
```

- Update the printer driver
- Test direct print vs through print server 

# Poor print quality

## Symptoms: Streaks, faded text, spots

## TroubleShooting Steps

- Run printer's cleaning cycle
- Check toner/ink quality
- Inspect paper tray for correct size/typ
- Replace cartridge/toner if neccessary

# Cannot find printer on Network

## Symptoms: Users can not discover printer

## TroubleShooting Step

- Confirm printer has an IP address assigned
- Verify it's on the same subnet as users
- Check DHCP server for reseevation conflicts
- Try connecting directly via IP:
    In Windows - ADD Printer -> ADD by IP Address

# Authentication and Access Issues

## Symptoms: User prompted for credentials, can not print

## TroubleShooting Step

- Verify printer share permissions in Active Directory or orint server
- Ensure user account is in the correct security group
- Remove and re-add the printer with correct credentials

# Frequent paper jams

## Symptoms: Printer stops with jam errors often

## TroubleShooting Steps

- Check rollers for debris/dust
- Confirm correct paper type
- Inspect tray alignment
- Escalate to maintenance if jams are reoccuring in same spot

# Using Printing to wrong printer

## Symptoms: Job shows up at another printer 

- Confirm the correct default printer is set
- Verifying the mapping in Active Directory Group Policy or script
- Check the printer's share name - similar names often cause mix- ups

# Drivers and Compatibility Errors

## Sumptoms: Printers not working after OS update

## TroubleShooting Steps

- Download the latest driver from manufacturer's site
- Remove old driver packages ( Print Management Console in Windows )
- Reinstall printer with updated driver


