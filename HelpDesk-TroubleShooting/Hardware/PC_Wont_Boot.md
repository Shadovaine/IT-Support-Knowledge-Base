# PC Booting Issues Playbook

## Common PC Issues

### Power Issues

- Power Supply (PSU) switch off or faulty
- Loose or disconnected power cables ( 24-pin ATX, 8-pin CPU, GPU )
- Bad wall outlet, power strip, or surge protector
- Dead CMOS battery

### Hardware Connections

- RAM not seated properly
- GPU not fully seated
- Loose storage ( HDD/SSD/NVMe )
- Front panel connectors miswired

### Perioheral Issues

- Faulty USB device preventing boot
- Stuck key on keyboard 
- Monitor unplugged or wrong input selected

### POST/BIOS Issues

- Incorrect BIOS setting
- Corrupted BIOS or failed update
- Overclocking instability

### Component Failure

- Bad RAM stick
- Dead GPU or CPU
- Failed PSU
- MotherBoard Failure

# TroubleShooting Steps

## Check Power

- Ensure PSU switch is ON
- Confirm outlet/power strip works
- Ispect PSU cables:
    24-pin ATX to motherboard
    8-pin CPU power
    GPU PCIe cables if present 
- If PSU is completely dead, try a different PSU

## Basic Startup Test

- Disconnect all peripherals ( USB, external drives, etc )
- Connect only KMM
- Press power button 
    - Fans spinning
    - LEDs lighting up
    - Any beeps

## Check Monitor and Display

- Verify monitor is ON and set to the correct input
- Reseat GPU
- Test another cable/monitor 

## Reseat Key Components

- Power down, unplug PSU, hold power button 10 secs to discharge
- Reseat
    - RAM ( try one stick at a time in different slots )
    - GPU
    - Storage device
- Double check front panel connectors( especially PWR SW )

## Listen for Beep Codes and Check LEDs

- Some boards use LEDs for CPU/DRAM/VGA/BOOT
- If a soeaker is available, listen for beep codes -> check owners manual for meaning

## Clear CMOS

- Power off, unplug PSU
- Remove CMOS battery for 5 mins
- Reinstall -> try powering on again

## Test Components Individually

- Boot with only CPU + 1 stick RAM + onboard graphics
- Add components one by one until failure repeats
- Swap/test spare parts if available 


   