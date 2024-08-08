# Overview
**OneShot-Extended** performs the [Pixie Dust attack](https://forums.kali.org/showthread.php?24286-WPS-Pixie-Dust-Attack-Offline-WPS-Attack) without special card or monitor mode.

# Features
 - [Pixie Dust attack](https://forums.kali.org/showthread.php?24286-WPS-Pixie-Dust-Attack-Offline-WPS-Attack)
 - Offline WPS PIN generating algorithm
 - [Online WPS bruteforce](https://sviehb.files.wordpress.com/2011/12/viehboeck_wps.pdf)
 - Wi-Fi scanner with highlighting based on iw;
 - Ability to save upon success

# Requirements
 - Python 3.6 and above
 - [WPA Supplicant](https://www.w1.fi/wpa_supplicant/)
 - [Pixiewps](https://github.com/wiire-a/pixiewps)
 - [iw](https://wireless.wiki.kernel.org/en/users/documentation/iw)

# Notice
> [!WARNING] 
> - This tool is intended for educational and authorized penetration testing purposes only.
> It is not designed for, and must not be used for, illegal activities such as hacking, unauthorized access, or causing damage to systems or networks.
> - By using this tool, you agree to use it responsibly and ethically, and to comply with all applicable laws and regulations.
> - The developer assumes no responsibility for any misuse of this tool.

# Usage
```
Required arguments:
    -i, --interface=<wlan0>  : Name of the interface to use

Optional arguments:
    -b, --bssid=<mac>        : BSSID of the target AP
    -p, --pin=<wps pin>      : Use the specified pin (arbitrary string or 4/8 digit pin)
    -K, --pixie-dust         : Run Pixie Dust attack
    -B, --bruteforce         : Run online bruteforce attack
    --push-button-connect    : Run WPS push button connection

Advanced arguments:
    -d, --delay=<n>          : Set the delay between pin attempts [0]
    -w, --write              : Write AP credentials to the file on success
    -s, --save               : Save the AP to network manager on success
    -F, --pixie-force        : Run Pixiewps with --force option (bruteforce full range)
    -X, --show-pixie-cmd     : Always print Pixiewps command
    --vuln-list=<filename>   : Use custom file with vulnerable devices list ['vulnwsc.txt']
    --iface-down             : Down network interface when the work is finished
    -l, --loop               : Run in a loop
    -r, --reverse-scan       : Reverse order of networks in the list of networks. Useful on small displays
    --mtk-wifi               : Activate MediaTek Wi-Fi interface driver on startup and deactivate it on exit
                               (for internal Wi-Fi adapters implemented in MediaTek SoCs). Turn off Wi-Fi in the system settings before using this.
    -v, --verbose            : Verbose output
 ```

# Installation
## Debian/Ubuntu
**Installing requirements**
 ```shell
 sudo apt install -y python3 wpasupplicant iw wget
 ```
**Installing Pixiewps**

***Ubuntu 18.04 and above or Debian 10 and above***
 ```shell
 sudo apt install -y pixiewps
 ```
 
**Getting OneShot**
 ```shell
 cd ~
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```shell
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/vulnwsc.txt
 ```
## Arch Linux
**Installing requirements**
 ```shell
 sudo pacman -S wpa_supplicant pixiewps wget python
 ```
**Getting OneShot**
 ```shell
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```shell
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/vulnwsc.txt
 ```
## Alpine Linux
It can also be used to run on Android devices using [Linux Deploy](https://play.google.com/store/apps/details?id=ru.meefik.linuxdeploy)

**Installing requirements**  
Adding the testing repository:
 ```shell
 sudo sh -c 'echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories'
 ```
 ```shell
 sudo apk add python3 wpa_supplicant pixiewps iw
 ```
 **Getting OneShot**
 ```shell
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/oneshot.py
 ```
Optional: getting a list of vulnerable to pixie dust devices for highlighting in scan results:
 ```shell
 wget https://raw.githubusercontent.com/chickendrop89/OneShot-Remastered/master/vulnwsc.txt
 ```
## [Termux](https://termux.com/)
Please note that root access is required.  

**Installing requirements**
 ```shell
 pkg install -y root-repo
 pkg install -y git tsu python wpa-supplicant pixiewps iw openssl
 ```
**Getting OneShot**
 ```shell
 git clone --depth 1 https://github.com/chickendrop89/OneShot-Remastered OneShot
 ```
#### Running
 ```shell
 sudo python OneShot/oneshot.py -i wlan0
 ```

## Usage examples
Start Pixie Dust attack on a specified BSSID:
 ```shell
 sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -K
 ```
Show avaliable networks and start Pixie Dust attack on a specified network:
 ```shell
 sudo python3 oneshot.py -i wlan0 -K
 ```
Launch online WPS bruteforce with the specified first half of the PIN:
 ```shell
 sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -B -p 1234
 ```
 Start WPS push button connection:s
 ```shell
 sudo python3 oneshot.py -i wlan0 --pbc
 ```

## Troubleshooting
#### "RTNETLINK answers: Operation not possible due to RF-kill"
 Just run:
```sudo rfkill unblock wifi```
#### "Device or resource busy (-16)"
 Try disabling Wi-Fi in the system settings and kill the Network manager. Alternatively, you can try running OneShot with ```--iface-down``` argument.
#### The wlan0 interface disappears when Wi-Fi is disabled on Android devices with MediaTek SoC
 Try running OneShot with the `--mtk-wifi` flag to initialize Wi-Fi device driver.

# Acknowledgements
## Special Thanks
* `kimocoder, drygdryg, chickendrop89` for extended implementation 
* `rofl0r` for initial implementation;
* `Monohrom` for testing, help in catching bugs, some ideas;
* `Wiire` for developing Pixiewps.
