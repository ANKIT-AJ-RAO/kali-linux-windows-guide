# 🐉 Kali Linux on Windows 10 & 11: Complete Installation Guide

A comprehensive, beginner-friendly guide to setting up Kali Linux on Windows 10 and Windows 11 using **Oracle VM VirtualBox** or **WSL 2 (Windows Subsystem for Linux)**.

---

## 📑 Table of Contents
1. [Prerequisites & System Verification](#-prerequisites--system-verification)
2. [Method Comparison](#-method-comparison)
3. [Method 1: VirtualBox Installation (Recommended)](#-method-1-virtualbox-installation-recommended)
4. [Method 2: WSL 2 Installation (Native Terminal & GUI)](#-method-2-wsl-2-installation-native-terminal--gui)
5. [Essential Post-Installation Commands](#-essential-post-installation-commands)
6. [Troubleshooting Common Issues](#-troubleshooting-common-issues)
7. [How to Save This Guide as a PDF](#-how-to-save-this-guide-as-a-pdf)
8. [Disclaimer](#-disclaimer)

---

## 📌 Prerequisites & System Verification

Before beginning the installation, ensure your computer meets the following hardware specs:

* **Operating System:** Windows 10 (Build 19041+) or Windows 11 (64-bit).
* **RAM:** 8 GB minimum (16 GB recommended for running VMs smoothly).
* **Free Storage:** At least 35 GB of free SSD/HDD storage.
* **Hardware Virtualization:** Must be enabled in BIOS/UEFI (**Intel VT-x** or **AMD-V**).

### How to Check if Virtualization is Enabled:
1. Press `Ctrl + Shift + Esc` to open **Task Manager**.
2. Switch to the **Performance** tab and click **CPU**.
3. Check the bottom-right details pane for **Virtualization: Enabled**.
4. If it states *Disabled*, restart your PC, press your BIOS key (`F2`, `F10`, `F12`, or `Del`), find **CPU Configuration**, and enable **Intel Virtualization Technology** or **SVM Mode**.

---

## ⚖️ Method Comparison

| Feature | Method 1: VirtualBox | Method 2: WSL 2 |
| :--- | :--- | :--- |
| **Best For** | Full Pentesting, Wi-Fi hacking, network isolation | Fast terminal access, CLI tools, lightweight use |
| **Isolation** | 100% sandboxed from Windows | Shares host kernel and network stack |
| **External USB Wi-Fi**| Supported (Direct USB Passthrough) | Complex / Limited USB support |
| **Resource Usage** | Higher (allocates dedicated RAM & CPU) | Minimal (dynamic resource allocation) |

---

## 🖥️ Method 1: VirtualBox Installation (Recommended)

### Step 1: Download the Required Software
* **VirtualBox & Extension Pack:** Download from [virtualbox.org](https://www.virtualbox.org/).
* **Kali Linux Pre-Built Image:** Visit [kali.org/get-kali](https://www.kali.org/get-kali/#kali-virtual-machines) and download the **VirtualBox 64-bit** (`.7z`) archive.
* **7-Zip Archive Utility:** Download from [7-zip.org](https://www.7-zip.org/) if you don't already have an archive extractor.

### Step 2: Install VirtualBox
1. Launch the downloaded VirtualBox installer and proceed through the setup wizard using default settings.
2. Double-click the downloaded **VirtualBox Extension Pack** and click **Install** to enable USB 2.0/3.0 controller support.

### Step 3: Extract and Launch Kali Linux
1. Right-click the downloaded Kali Linux `.7z` file > select **7-Zip** > **Extract to "kali-linux-..."**.
2. Open the newly extracted directory.
3. Double-click the blue `.vbox` file (e.g., `kali-linux-202X.X-virtualbox-amd64.vbox`). VirtualBox will automatically import and register the machine.

### Step 4: Configure Virtual Machine Resources
1. Select the Kali virtual machine in VirtualBox and click **Settings** (`Ctrl + S`).
2. Go to **System** > **Motherboard**: Set **Base Memory** to at least **4096 MB (4 GB)**.
3. Go to **System** > **Processor**: Allocate **2 to 4 CPU cores** (stay within the green slider limit).
4. Go to **Display**: Set **Video Memory** to **128 MB** and check **Enable 3D Acceleration**.
5. Click **OK**.

### Step 5: Boot Up and Log In
1. Click the green **Start** button in VirtualBox.
2. At the login screen, enter the default credentials:
   * **Username:** `kali`
   * **Password:** `kali`

---

## ⚡ Method 2: WSL 2 Installation (Native Terminal & GUI)

### Step 1: Enable WSL
1. Right-click the Windows Start menu and choose **Terminal (Admin)** or **PowerShell (Admin)**.
2. Run the following command:

    wsl --install

3. Restart your computer when prompted.

### Step 2: Install Kali Linux
1. Open PowerShell (Admin) and run:

    wsl --install -d kali-linux

2. When the installation completes, the console will prompt you to set a **UNIX username** and **password**.

### Step 3: Set Up Graphical Desktop (Win-KeX)
1. Inside the Kali WSL terminal, update packages and install Win-KeX:

    sudo apt update && sudo apt install -y kali-win-kex

2. To start the desktop interface in windowed mode with audio support:

    kex --win -s

3. To stop the GUI session when finished:

    kex --stop

---

## 🛠️ Essential Post-Installation Commands

Open your terminal inside Kali (`Ctrl + Alt + T`) and run these maintenance tasks immediately:

### 1. Update Package Repositories and System Software

    sudo apt update && sudo apt full-upgrade -y

### 2. Change the Default Password (For VirtualBox Users)

    passwd

### 3. Clean Obsolete Cache Files

    sudo apt autoremove -y && sudo apt clean

---

## 🔧 Troubleshooting Common Issues

* **Issue: "VT-x/AMD-V hardware acceleration is not available on your system"**
  * **Fix:** Restart your machine, enter BIOS/UEFI setup, locate CPU features, and turn on virtualization (**Intel VT-x** or **AMD SVM**). Also ensure Windows Hyper-V isn't conflicting by running `bcdedit /set hypervisorlaunchtype off` in Administrator CMD if VirtualBox fails to start.

* **Issue: VirtualBox screen is tiny and does not auto-resize**
  * **Fix:** In the VirtualBox top menu bar, navigate to **View** > click **Auto-resize Guest Display**. If grayed out, install guest additions inside Kali using:

    sudo apt update && sudo apt install -y virtualbox-guest-x11
    sudo reboot

* **Issue: WSL 2 error "WslRegisterDistribution failed with error: 0x80370102"**
  * **Fix:** Enable virtualization in BIOS and verify the "Virtual Machine Platform" Windows feature is turned on:

    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

---

## 📄 How to Save This Guide as a PDF

1. Open this repository page in Google Chrome, Microsoft Edge, or Brave.
2. Press `Ctrl + P` (Print).
3. Under **Destination**, select **Save as PDF**.
4. Set **Pages** to **All** and check **Background graphics** under More settings.
5. Click **Save**.

---

## ⚖️ Disclaimer
*This guide and its contents are intended solely for educational purposes, security research, and authorized penetration testing. Do not use these tools on systems without explicit permission.*
