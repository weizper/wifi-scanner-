# wifi-scanner-
A Wi-Fi scanner is a tool that detects nearby wireless networks, analyzes signal strength, and identifies channel congestion to help optimize your network connection

import subprocess
import platform

def scan_wifi():
    system_platform = platform.system()

    if system_platform == "Windows":
        # Use netsh command on Windows
        networks = subprocess.check_output(["netsh", "wlan", "show", "network", "mode=Bssid"], encoding="utf-8")
        print(networks)

    elif system_platform == "Linux":
        # Use nmcli command on Linux
        networks = subprocess.check_output(["nmcli", "-t", "-f", "SSID,SIGNAL", "dev", "wifi"], encoding="utf-8")
        print("Available Wi-Fi Networks:")
        for line in networks.strip().split("\n"):
            ssid, signal = line.split(":")
            print(f"SSID: {ssid}, Signal Strength: {signal}%")

    elif system_platform == "Darwin":  # macOS
        # Use airport command on macOS
        networks = subprocess.check_output(
            ["/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport", "-s"],
            encoding="utf-8"
        )
        print(networks)

    else:
        print("Unsupported Operating System")

if __name__ == "__main__":
    scan_wifi()
