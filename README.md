# WSL Setup for Ubuntu (RUN Linux on windows)

**Enable Hyper-V to run Virtual Machine on a windows hardware device.** 
###Follow instruction from this URL
https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v


**Install WSL on windows.**
**Follow instruction from this URL**
https://docs.microsoft.com/en-gb/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package

**OR**

**Installation Steps**
If you are not on a Windows Insiders build, the features required for WSL will need to be enabled manually following the steps below.

**Step 1 - Enable the Windows Subsystem for Linux**
You must first enable the "Windows Subsystem for Linux" optional feature before installing any Linux distributions on Windows.

Open PowerShell as Administrator and run:
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

We recommend now moving on to step #2, updating to WSL 2, but if you wish to only install WSL 1, you can now restart your machine and move on to Step 6 - Install your Linux distribution of choice. To update to WSL 2, wait to restart your machine and move on to the next step.

**Step 2 - Check requirements for running WSL 2**
To update to WSL 2, you must be running Windows 10.

For x64 systems: Version 1903 or higher, with Build 18362 or higher.
For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.
Builds lower than 18362 do not support WSL 2. Use the Windows Update Assistant to update your version of Windows

**Step 3 - Enable Virtual Machine feature**
Before installing WSL 2, you must enable the Virtual Machine Platform optional feature. Your machine will require virtualization capabilities to use this feature.

Open PowerShell as Administrator and run:
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
Restart your machine to complete the WSL install and update to WSL 2.**

[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi]()

**Step 4 - Set WSL 2 as your default version**
Open PowerShell and run this command to set WSL 2 as the default version when installing a new Linux distribution:
```
wsl --set-default-version 2
```

**Step 5 - Install your Linux distribution of choice**
Open the Microsoft Store and select your favorite Linux distribution.

[WSL Store](https://aka.ms/wslstore)

Ubuntu 16.04 LTS

**Step 6 - Enable DNS that comes from VPN to be enabled for WSL**

It is known issue with WSL that DNS coming from the VPN network is not reflected in WSL machine.

“/etc/resolv.conf” are automatically generated when WSL is turned on. In most of the WSL distributions, this file is linked with other file.

Follow the steps below in order to place custom DNS server address including VPN DNS server:

**Step A : Copy the existing resolv.conf and disable the auto generation of the resolv.conf on Ubuntu or distribution you are running**
```
sudo cp /etc/resolv.conf /etc/resolv.conf.bk
```

To disable the auto-generation of the resolv.conf. Create or edit **/etc/wsl.conf** with the following content:
```
[network]
generateResolvConf = false
```

**Step B : Unlink existing resolv.conf**
```
sudo unlink /etc/resolv.conf
```

**Step C** : 
Edit and save the /etc/resolv.conf with the DNS server entries you need, can reference to the DNS entries collected from the Step 1.
You can add custom VPN DNS entries as well like GOOGLE DNS as mentioned in the next step, which will make sure when you connect to the VPN, DNS resolution will work.

Add google DNS (nameserver 8.8.8.8) entry to resolv.conf file

```
sudo vi /etc/resolv.conf

nameserver 8.8.8.8

```

**Docker Setup on WSL2 to run apps on the containers**
Refer this link to setup docker desktop on windows [Link](https://code.visualstudio.com/blogs/2020/03/02/docker-in-wsl2)

**OR**

```
**Install Docker in WSL Ubuntu**

Follow the usual installation instructions to install Docker Desktop. ...

Start Docker Desktop from the Windows Start menu.

From the Docker menu, select Settings > General.

Select the Use WSL 2 based engine check box.

Click Apply & Restart.

Ensure the distribution runs in WSL 2 mode.

```
