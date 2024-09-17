# rtl8188gu-kali-setup
# RTL8188GU on Kali Linux
This repository provides the missing firmware file (rtl8710bufw_SMIC.bin) required for the RTL8188GU Wi-Fi chipset on Kali Linux. Although Kali Linux includes the driver (rtl8xxxu) by default, it does not come with the necessary firmware file for the RTL8188GU chipset.

Overview
If your Wi-Fi adapter uses the RTL8188GU chipset and it is not functioning on Kali Linux, it’s likely due to a missing firmware file. The driver (rtl8xxxu) is already included in the Linux kernel, but without the firmware, the adapter won’t work.

This repository contains the required .bin firmware file and instructions to get your adapter up and running.

Steps to Set Up RTL8188GU on Kali Linux

# 1. Download the Firmware
First, download the rtl8710bufw_SMIC.bin file from this repository.

Using wget:

wget https://github.com/Malik24626/rtl8188gu-kali-setup/raw/main/rtl8710bufw_SMIC.bin

# 2. Install the Firmware
Copy the downloaded firmware file to the system firmware directory (/lib/firmware/rtlwifi/):

sudo cp rtl8710bufw_SMIC.bin /lib/firmware/rtlwifi/

# 3. Load the Driver
Once the firmware is in place, you need to load the rtl8xxxu module (driver). The driver is already included in Kali Linux, so there’s no need to compile or install it separately.

To load the driver:

sudo modprobe rtl8xxxu
This command loads the driver into the kernel, allowing the Wi-Fi adapter to be recognized.

# 4. Set the Driver to Load at Boot (Optional)
To avoid manually loading the driver every time you reboot, you can configure the system to automatically load it at boot. Add the driver to /etc/modules:

Edit the file:

sudo nano /etc/modules
Add the following line at the end:

rtl8xxxu
Save and exit (Ctrl+X, then Y, then Enter).

# 5. Reboot and Verify
Reboot your system to ensure everything is working:

sudo reboot
After rebooting, you can check if the driver and firmware are loaded by running:

dmesg | grep rtl8xxxu
You should see messages indicating that the firmware was successfully loaded and the adapter is functioning.

Troubleshooting
Driver Not Loading Automatically: If the driver is not loaded after reboot, double-check that the firmware file is in the correct directory (/lib/firmware/rtlwifi/) and that rtl8xxxu is listed in /etc/modules.
Device Not Detected: Ensure the Wi-Fi adapter is plugged in properly and recognized by the system using the lsusb command:

lsusb
Conclusion
With this setup, your RTL8188GU Wi-Fi adapter should work seamlessly on Kali Linux. The included driver in the kernel (rtl8xxxu) combined with the rtl8710bufw_SMIC.bin firmware allows full functionality of the adapter.

If you run into any issues or have questions, feel free to open an issue on this repository!

