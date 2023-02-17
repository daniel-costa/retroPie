# RetroPie Emulator Gaming System

## Quick Reference 

### Hotkey actions

| Action | Keys |
| ------ | ---- |
| Quit game | Hotkey + Start |
| Reset game | Hotkey + X |
| RetroArch menu (required for changing discs) | Hotkey + Δ |
| Save to emulator save slot | Hotkey + R1 |
| Load from emulator save slot | Hotkey + L1 |
| Increase emulator save slot number | Hotkey + right |
| Decrease emulator save slot number | Hotkey + left |
| Volume up (must be configured first) | Hotkey + up |
| Volume down (must be configured first) | Hotkey + down |

### Changing discs

1. Open RetroArch menu (Hotkey + Δ)
2. Open "Quick Menu" if not already open
3. "Disc Control" (near the bottom of the list)
4. "Eject disc"
5. "Load new disc"
6. Select disc to load

### Add volume control to a controller

1. Exit EmulationStation
	1. Start
	2. "Quit"
	3. "Quit EmulationStation"
2. `cd ~/.config/retroarch/autoconfig`
3. For every controller configuration file here ending in `.cfg` (don't need to worry about the `.cfg.bak` files):
	1. `sudo nano FILENAME.cfg`
	2. Add these two lines 
		- `input_volume_up_btn = "h0up"`
		- `input_volume_down_btn = "h0down"`

## Controller Diagrams

### NES (Nintendo Entertainment System)

![NES Controller](./images/controller_nes.png?raw=true "NES Controller")

### Super Nintendo Entertainment System (SNES)

![SNES Controller](./images/controller_snes.png?raw=true "SNES Controller")

### Nintendo 64

![N64 Controller](./images/controller_n64.png?raw=true "N64 Controller")

### Playstation

![PSX Controller](./images/controller_psx.png?raw=true "PSX Controller")

## Instructions

### Parts:
- [Raspberry SC15184 Pi 4 Model B (2GB)](https://a.co/d/9vqdlMV)
- [Logitech K400 Plus Wireless Touch TV Keyboard](https://a.co/d/eNKBeEi)
- [GeeekPi Raspberry Pi 4 Case with Cooling Fan and Heatsinks](https://a.co/d/21P8Awb)
- [LESOWN 7 inch Monitor with Speakers](https://a.co/d/aM4b5PF)
- [SanDisk 64GB MicroSD Card](https://a.co/d/3vjeQkB)
- [Monitor stand](https://www.amazon.com/dp/B08RNBRCSV)
- [HDMI to micro HDMI cable](https://a.co/d/bviJpxo)
- [Raspberry Pi 4 power supply](https://www.digikey.com/en/products/detail/raspberry-pi/RPI-USB-C-POWER-SUPPLY-BLACK-AUS/10258763?src=raspberrypi)


### Steps:
1. Check all required parts are available
	- SD card reader
	- SD card
	- Raspberry Pi board, power supply, and case
	- Keyboard / mouse
	- Monitor and cables
	- Game controller and cable
2. Flash the SD  card so it can run RetroPie / EmulationStation
	1. Insert the SD card into the computer
	2. Install and launch [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
	3. Flash the SD card with the RetroPie image
		1. Choose RetroPie for the Raspberry Pi 4 as the OS
			- "Emulation and game OS"
			- "RetroPie"
			- "RetroPie 4.8 (RPI 4/400)"
		2. Choose the SD card as the installation location
		3. Click "Write"
3. Assemble the hardware (see case instructions)
	1. Apply thermal stickers to the heat sinks and install them on the Raspberry Pi chips
	2. Screw the Raspberry Pi into the case (similar to wood screws, not bolts. They can be hard to screw in, be careful)
	3. Wire the fan into the GPIO pins
4. Initial Retro Pie auto-setup
	1. Insert SD card into the Raspberry Pi
	2. Connect monitor and keyboard/mouse
	3. Connect controller
	4. Boot the system by connecting the power
	5. Wait for initial auto-setup
5. Connect controller and setup mapping
	- Hold any button on the controller to start mapping
6. Open the "RetroPie" menu option so we can start setting up the system
7. General system setup
	1. Use the controller to select "Raspi-config", but you will need to use the keyboard for the below
	2. Set the Wi-Fi country, we'll connect to Wi-Fi later
		1. "System Options"
		2. "Wireless LAN"
		3. "Australia"
		4. "Cancel"
	3. Fix display underscan to remove black borders and use the full monitor
		1. "Display Options"
		2. "Underscan"
		3. "No"
		4. "Ok"
	4. Enable SSH so we can access it remotely
		1. "Interface Options"
		2. "SSH"
		3. "Yes"
		4. "Ok"
	5. Set keyboard layout to US because it defaults to UK 
		1. "Localisation Options"
		2. "Keyboard"
		3. "Generic 105-Key PC (intl)"
		4. "Other"
		5. "English (US)"
		6. "English (US)"
		7. "The default for the keyboard layout"
		8. "No compose key"
	6. Exit back to EmulationStation
		1. Select "Finish"
		2. "No", **Don't** reboot yet
8. Connect to Wi-Fi so we can download software when required
	1. Select "WiFi"
	2. "Connect to WiFi network"
	3. Select the network from the list
	4. Enter the password (either using the keyboard or the controller)
	5. "OK", then wait
	6. "Exit"
9. Additional setup
	1. Use the controller to select "RetroPie setup" (you can use the controller for the below)
	2. Install a desktop environment so we can use the Raspberry Pi like a normal computer if we want to.
		1. Start the installation
			1. "Configuration / tools" (C)
			2. "raspbiantools" (219)
			3. "Install Pixel desktop environment"
			4. "Yes"
		2. Wait. **This can take a long time, anywhere from 5 to 40 mins**
		3. Select "OK"
		4. Remove software we don't need; otherwise, this can cause audio issues
			- "Remove some unneeded packages"
		5. "Cancel"
	3. Update menu controls so "X" is enter and "O" is exit
		1. "emulationstation" (205)
		2. "Swap A/B buttons" (3)
		3. "Ok"
	4. Exit back to EmulationStation
		1. "Cancel"
		2. "Back"
		3. "Exit"
	5. Reconfigure controller (required after updating the menu controls)
		1. Start
		2. "Configure Input"
10. Final setup tweaks
	1. Exit EmulationStation
		1. Start
		2. "Quit"
		3. "Quit EmulationStation"
	2. Edit the configuration file so it always thinks the display has audio and video
		1. `sudo nano /boot/config.txt`
		2. Remove the "`#`" from "`#hdmi_drive=2`"
		3. Exit and save: 
			1. `Ctrl + x`
			2. `y`
			3. `Enter`
	3. Add hotkey volume control for each controller so you can easily change the volume while playing
		1. `cd ~/.config/retroarch/autoconfig`
		2. For every controller configuration file here ending in `.cfg` (don't need to worry about the `.cfg.bak` files):
			1. `sudo nano FILENAME.cfg`
			2. Add these two lines 
				- `input_volume_up_btn = "h0up"`
				- `input_volume_down_btn = "h0down"`
11. Make sure everything is fully up to date
	1. Run the below update command
		- `sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade`
	2. Wait. **This can take a long time, anywhere from 5 to 25 mins**
12. Reboot so changes take effect and things aren't as slow
	- `sudo reboot now`
13. Transfer the games and BIOS
	1. Open desktop
		1. "Ports"
		2. "Desktop"
	2. The USB drive and monitor take a lot of power. Temporarily power the monitor from a separate source like your laptop and disconnect the controller/s
	3. Insert the USB drive into one of the blue USB ports (they're faster)
	4. Open file manager when prompted
	5. Open the BIOS folder and copy everything into:
		-  "Home folder" ==> "RetroPie" ==> "BIOS"
	6. Copy everything in the "roms" folder into 
		-  "Home folder" ==> "RetroPie" ==> "roms"
		- When prompted:
			- "Apply this option to all existing files"
			- "Overwrite"
	7. Wait. **This can take a REALLY long time, anywhere from 15 to 70 mins**
	8. When copying the files is finished, eject the USB drive
14. Install Scratch (fun coding program)
	1. Open a terminal window by clicking the black box in the top menu bar
	2. Install Scratch
		1. `sudo apt install scratch -y`
	3. Scratch projects: 
		1. https://projects.raspberrypi.org/en/pathways/scratch-intro
		2. https://projects.raspberrypi.org/en/codeclub/
15. Reboot so EmulationStation can find the new games
	1. Open the start menu by clicking the raspberry in the top-left
	2. "Shutdown"
	3. "Reboot"
16. Now that we have games, we can get  artwork and details for them
	1. Start scraping for everything but "Ports" (scrapes "Desktop" as a "Desktop Dungeon" game)
		1. Start
		2. "Scraper"
		3. "Scrape now"
		4. "Filter"
			1. "All games"
			2. "Back"
		5. "Systems"
			1. Deselect "Ports"
			2. "Back"
		6. Set "User decides on conflicts" to "Off"
		7. "Start"
	2. Wait (this shouldn't take too long, about 5 mins)
	3. Select "OK"
	4. Close the menu
17. Scraping isn't perfect, and we need to update some of the games
	- How to manually update the scraped information:
		1. Highlight the incorrectly-named game
		2. Press the "Select" button
		3. "Edit this game's metadata"
		4. "Scrape"
		5. Select the correct game
		6. "Save"
		7. Close the window
	- Games that need to be manually changed:
		- Nintendo 64
			- Banjo to Kazooie No Daibouken ==> Banjo-Kazooie
			- Blastdozer ==> Blast Corps
			- Lylat Wars ==> Star Fox 64
			- Star Wars: Teikoku No Kage ==> Star Wars: Shadows of the Empire
		- SNES
			- Super Donkey Kong ==> Donkey Kong Country
			- Akumajo Dracula ==> Super Castlevania IV
			- SMW2+ ==> Super Mario World 2: Yoshi's Island
			- Panel De Pon ==> Tetris Attack
		- Playstation
			- Crash Bandicoot 2 - Cortex No Gyakushuu! ==> Crash Bandicoot 2: Cortex Strikes Back
			- Oddworld: Abe's Exoddus ==> Oddworld - Abe's oddysee
18. Add the "Last Played" collection so you can easily reopen what you were last playing
	1. Start
	2. "Game collection settings"
	3. "Automatic game collections"
	4. "Last played"
19. Turn off vibration because it draws too much power and causes issues with the screen
	1. Launch any Playstation game
	2. Open RetroArch quick menu (Hotkey + Δ)
	3. Open "Quick Menu" if not already open
	4. "Options"
	5. "Enable Vibration" ==> "Off"
20. Clean up boxes, rubbish, etc.
21. Play!
