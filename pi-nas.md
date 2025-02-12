# The ultimate Raspberry Pi NAS build for 2025!

[The ultimate Raspberry Pi NAS build for 2025!](https://www.youtube.com/watch?v=xYqkfYmJJ6w)


Today we're discussing how to turn our Raspberry pi 4b into an affordable Network Attached storage, NAS, solution so we can share files on our network!
NAS appliances, like Synology's Diskstations or QNAP can be quite expensive for just the dedicated hardware and you still need to purchase storage drives! 
Free solutions like TrueNAS is certainly a good options if you already have sufficient hardware, but there's quite the learning curve to utilize TrueNas to its full potential!
The good news is there are more accessible options like Open Media Vault, OMV, which is a free open sourced based NAS solution based off Linux.
As we'll discuss, OMV can be installed via ISO as a stand alone NAS solution, (similar to TrueNAS) but we'll install it on a Raspberry 4b running Raspberry Pi OS lite on a 32GB Micro-SD card.
After the installation on the pi, we'll peruse OMV, configure the storage drive and folder shares, assign users and then test it out on our Mac and iPhone!

## Chapter Markers:
  0:00 Introduction
  1:01 What is Open Media Vault
  1:31 Agenda for Video
  2:17 Format the SD Card, installing Raspberry Pi Imager
  2:55 Flashing 32GB Micro-SD card with Raspberry pi OS Lite
  4:11 Locating the Raspberry Pi's IP Address with iOS Network Analyzer
  4:34 Updating the Raspberry Pi's OS
  5:38 Installing OMV Scripts
  7:03 Logging into OMV for the first time.
  7:40 Configuring OMV's dashboard
  8:53 Exploring OMV's network, storage, sharing, and user options
  10:21 Raspberry Pi Power requirements 
  10:55 Configuring the 500GB USB HDD and 'File Systems'.
  12:07 Configuring 'Shared Folders' 
  12:45 User Creation
  13:45 Configuring file/folder sharing services/protocols
  14:30 Assigning Shared folders with sharing services
  15:57 Accessing shared folder on the network through our Mac
  17:43 Accessing shared folder on the network through our iPhone
  19:21 Conclusion

## Here's what you need to get started:
*Make sure you have an additional USB SSD (linked below) as OMV will utilize the entirety of the Micro-SD card and you cannot partition or allocate it for any additional 'storage'.
*To run OMV, you need at least a Raspberry pi 2b, but we're going to be using a Rapsberry pi 4b (linked below).
*As an aside, if your external USB storage drive doesn't have it's own power supply (such as my situation), make sure you're using a 5v USBC-power adapter for your Raspberry pi (I have links below for 'kits' and a stand alone power supply). In any case, it's recommended to use a USB SSD drive so your Raspberry pi power requirements are minimal.

➡️ 6ft HDMI to Mini HDMI for connection of the Raspberry pi 4B to a monitor.https://a.co/d/aLFUlK5
➡️ Raspberry 4b (complete kit  includes Micro-Sd card and 5v power supply) https://a.co/d/bYbrVSI
➡️ [Raspberry Pi 4b 5v power supply ONLY] (https://a.co/d/fB5Yz2q)
➡️ [32GB 2x pack Micro-Sd cards with SD adapter] (https://a.co/d/bI1VEgS)
➡️ [USB SSD storage (I used an HDD](https://a.co/d/hFdT6ip)
➡️ [Raspberry Pi Imager to install Pin OS Lite] (https://www.raspberrypi.com/software/)
➡️ [SD Formating Tool] (https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbGlPNExoWHFOcDlxZGtDRVJ6bVZGOGNhMlZwUXxBQ3Jtc0trY0RTV1FvbnZGaWFZaE85NXFrUjAyUjVJYWFHRHRBdkxqZi1OYTFPbWgwR0ZTZjdZZHJxbk9HeHdBaUh3NGYzNzdNWWJtMl9rem8zQUk5VjhJMVNMVmxXc0Q1RkVZUlRnUTlxQWZGSk93Y3pTRFRxbw&q=https%3A%2F%2Fwww.sdcard.org%2Fdownloads%2Fformatter%2F&v=xYqkfYmJJ6w)
➡️ Open Media Vault Download (Use ONLY if you're retrieving the ISO) (https://www.openmediavault.org)

### SSH Tools (Optional)
[Putty for Windows (for Mac/ Linux, the terminal works fine for SSH!](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbGVvV0FXYkhLWkpGckJOdzA3Rnl3dXF0bDc4QXxBQ3Jtc0trWllKcUtGN0tUcmdzQlVZT2dRellZaURLTFVjTEh4d196WXoyeC1JUDhmUUQ4OWI4VVJmVkJCa284cnpMR2Radm1BT0tzR1BJRTZtbUhrVTU4Ymo2ZFQ3clhmVGVwd3VESlgyNWxlbjBIU2cySzBfRQ&q=https%3A%2F%2Fwww.chiark.greenend.org.uk%2F%7Esgtatham%2Fputty%2Flatest.html&v=xYqkfYmJJ6w)
➡️ [Find your Raspberry Pi on your network with Network Analyzer] (https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbGRwNFoxT0g5UWQ3MEk0cjVHVVF5X1BpV2F1UXxBQ3Jtc0tsQy1nbmN4a3h2YVJCN1lOQzUycTNtZVY4Z1ZEeDVJZHpPQlJOZ1hmWXdzaUJmdjdzaFZOX1k4QndYa0duQW1aTG00a2NOcHRJb0ZDWEFScWU2dDE2SExKNS1EbU1LRDNtTE1wR3FUTFNPRnBIY3Y4Yw&q=https%3A%2F%2Fapps.apple.com%2Fus%2Fapp%2Fnetwork-analyzer-net-tools%2Fid562315041&v=xYqkfYmJJ6w)

## Raspberry Pi OMV Installation steps :
```bash
1. Update your raspberry pi's software
 1. 'sudo apt update && sudo apt-upgrade'
2. Reboot the pi
 1. 'sudo reboot'
3. Retrieve your pi's IP address
 1. 'hostname -i'
4. Download and install the OMV 'Preinstaller'
 1. wget -O - https://github.com/OpenMediaVault-Plu... | sudo bash
5. Reboot the pi
6. Download and install the OMV installer
 1. wget -O - https://github.com/OpenMediaVault-Plu... | sudo bash
7. Reboot the Pi one more time.
8. Open a computer browser (make sure it's on the same network as the pi) and enter the pi's IP address from step 3.
9. The default user name for OMV is:
 1. username: 'admin'
 2. password: 'openmediavault
```

## Videos on Network Attached Storage
1. Meet the NAS, Technology's Swiss arm knife
        • Meet the NAS, Technology's Swiss Army...  
2. Tired of logging into your NAS, watch this!
        • Tired of logging into your NAS for yo...  
