# retroPi

### Parts:
- Raspberry SC15184 Pi 4 Model B 2019 Quad Core 64 Bit WiFi Bluetooth (2GB) https://a.co/d/9vqdlMV
- Logitech K400 Plus Wireless Touch TV Keyboard With Easy Media Control and Built-in Touchpad, HTPC Keyboard for PC-connected TV, Windows, Android, Chrome OS, Laptop, Tablet - Black https://a.co/d/eNKBeEi
- GeeekPi Raspberry Pi 4 Case, Raspberry Pi 4 Case with Cooling Fan, Raspberry Pi 4 Heatsink, Retro Gaming Nes4Pi Case for Raspberry Pi 4 Model B/4B https://a.co/d/21P8Awb
- LESOWN 7 inch Monitor IPS Mini LCD Display Second Screen 1024x600 HDMI Small Portable Computer Monitor with Dual Speakers Audio Jack Metal Case https://a.co/d/aM4b5PF
- SanDisk 64GB Ultra microSDXC UHS-I Memory Card with Adapter - Up to 140MB/s, C10, U1, Full HD, A1, MicroSD Card - SDSQUAB-064G-GN6MA https://a.co/d/3vjeQkB
- MoKo Phone/Tablet Stand, Foldable Tablet Holder Compatible with iPhone 13 Pro Max/13 Pro/13, iPhone 12/12 pro Max/11/Xs Max, iPad Pro 11, iPad Air 4/Mini 6 2021, iPad 9th 10.2", Black https://a.co/d/0fE70XK
- JSAUX Mini HDMI to HDMI Cable 3FT, [Aluminum Shell, Braided] High Speed 4K 60Hz HDMI 2.0 Cord, Compatible with Camera, Camcorder, Tablet and Graphics/Video Card, Laptop, Raspberry Pi Zero W -Grey… https://a.co/d/bviJpxo
- Power supply: https://www.digikey.com/en/products/detail/raspberry-pi/RPI-USB-C-POWER-SUPPLY-BLACK-AUS/10258763?src=raspberrypi

### Notes: 
- The listed monitor can be powered from Pi. Single source makes it easy and it can be used in the car.
- Monitor also comes with an HDMI cable that should work
- Case comes with a fan and heatsinks, but not thermal paste. Overkill, but shows them what they need to do for real PCs

### Steps:
1. Check all required parts are available
	- SD card reader
	- Pi SD card
	- Pi board, power supply, and case
	- Keyboard and mouse
	- Monitor and cables
	- Game controller
2. Prepare SD  card
	1. Install Raspberry Pi Imager
	2. Flash card with RetroPi image
		- Choose RetroPi for the Pi 4 as the OS
		- Choose SD card as the installation location
3. Assemble hardware (see case instructions)
	1. Apply thermal stickers to Pi chips, install heatsinks
	2. Put Pi in case, screw in screws (similar to wood screws, not bolts. They can be hard to screw in, be careful)
	3. Wire fan into GPIO 
4. Initial Pi setup
	1. Insert SD card
	2. Connect monitor and keyboard/mouse
	3. Boot the system by connecting the power
	4. Wait
5. System setup (some steps take a long time, do next steps simultaneously via SSH where possible)
	1. Connect controller and setup mapping
	2. Open RetroPie menu option
	3. Raspi-config
		1. Setup wifi (1=>S1)
			1. Set to Australia
			2. Enter SSID
			3. Enter password
		2. Fix display overscan (2=>D2=>No)
		3. Enable SSH (3=>P2)
		4. Set keyboard layout (5=>L3=>Generic 104-key PC (intl)=>Other=>English US=>English US=>Default=>No compose)
		5. Finish
		6. No reboot
	4. RetroPie setup
		1. Install desktop environment
			1. Configuration / tools (C) => raspbiantools (219) => Install Pixel desktop environment
			2. Configuration / tools (C) => raspbiantools (219) => Remove unneeded packages (audio will not be sent to HDMI otherwise)
			3. Can be run using startx on command line or from the "Ports" console
		2. Update menu controls
			1. Manage packages (P) => Core (C) => emulationstation (205) => Configuration / options (C) => Swap A/B buttons (3)
			2. Exit
			3. Reconfigure controller (required after swapping A/B buttons)
	5. Display setup / update
		1. Exit emulationstation
		2. nano /boot/config.txt
			- hdmi_drive=2
		3. sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade
		4. sudo reboot now
	6. Confirm
		1. Screen is full size
		2. Audio comes from both monitor and 3.5mm jack (see below for instructions on how to switch audio output)
		3. Can launch desktop environment (Ports => Desktop or startx from command line)
6. Emulator setup <need to write instructions for Windows> <Upload to GDrive and share the link, download in Pi desktop?> <Put them on a thumb drive and include setting up SSH?>
	1. Open a terminal window
		- Windows: Windows + r ==> "cmd"
		- OSX / Linux: Terminal
	2. Transfer BIOS
		- NES, SNES, and N64 don't require BIOS
		- From directory with BIOS:
			- scp ./* pi@192.168.1.43:/home/pi/RetroPie/BIOS
	3. Transfer games
		- From directory with subdirectories  of nes, snes, n64, psx, etc:
			- scp -r ./* pi@192.168.1.43:/home/pi/RetroPie/roms
	4. Scrape artwork and details
		1. Menu => Scraper =>  Scrape now => User decides on conflicts (off) => Start
	5. Reboot
	6. Test one game on each platform (launches, has audio, video is the right size, responds to controls, save games persist <just NES, Tetris?>)
7. Optional: Setup Bluetooth connection (will affect how controllers can be used with Playstation)
	1. Open RetroPie menu option
	2. "Bluetooth"
	3. <need to write instructions>
8. Play
