# Peripheral Issues Playbook

## Peripherals consist of: keyboard, mouse, monitor, printer, USB drives, webcams, headsets, and others all connected to a PC

# Most Common Peripheral Issues

## Keyboard and Mouse

- Device not recognize ( USB not regnized )
- Keys not working and ghost typing
- Wireless input lag or no response
- Sticky and/or stuck keys

## Monitor and Displays

- "No Signal" message.
- Wrong resolutions or scaling
- Flickering, artificats, or color issues
- Black screen but PC is running 

## Printers

- Not showing up in OS
- Jobs stuck in queue
- Network printer unreachable
- Paper Jam, low ink/toner, dirty roller

## USB devices ( Storage, Webcam, etc. )

- Device not detected/ intermittent connection
- Drive letter not assigned
- Power-hungry device disconnected
- Conflicts with other USB devices 

## Audio Devices ( Headphones, Speakers, Misc. )

- No Sound/ No mic input 
- Wrong default playback/recording device
- Distorted Audio/ buzzing
- Bluetooth not pairing

# TroubleShooting Steps

## Basic Checks

- Verify device is plugged in firmly
- Test on a different USB port / cable
- Try the device on another computer to rule out hardware failure
- If wireless, check batteries are charged.

## Power and Ports

- for USB: unplug/replug, try different ports
- If device requires externalpower ( e.g. some drives/printers ) - check adapter
- Avoid cheap USB hubs - plug directly into PC for testing

## Drivers and OS

- Open Device Manager (Windows) or `lsusb` / `dmesg` ( Linux ) to see if its detected
- Update or reinstall drivers
- For printers, re-add the printer in Settings -> Devices -> Printers
- Install vendor software if needed

## Settings

- keyboard/Mouse: check language/ input settings
- Monitor: Confirm input source (HDMI, DP, VGA ). try another cable
- Audio: right-click sound icon -> select correct playback/recording device
- Printer: Set as default, clear print queue

## Conflicts and Firmware

- Unplug other peripherals to rule out conflicts
- Update device firemware if available
- for bluetooth devices, remove pairing and reconnect

## System-Level Fixes

- Restart PC ( resets driver stack )
- For USB power issues: disable "USB selective suspend" in Windows Power Options
- On Linux: reload drivers with `sudo modprobe -r <driver> && sudo modprobe`

## Replace and Repair

- Swap with a known-good cable or device
- If still failing ->  device hardware fault