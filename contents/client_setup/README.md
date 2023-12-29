# Setting Up Client Computer

### Table of Contents

[Setting Up Client Computer Virtual Machine](#setting-up-client-computer-virtual-machine)

[Adding Client Machine to Active Directory](#adding-client-machine-to-active-directory)

[Sections](#sections)

## Setting Up Client Computer Virtual Machine

Now that the computer objects are added to AD, the next step is to connect a Windows 10 client computer to the AD computer object. To test the functionality of group policies, we will be creating 3 different client virtual machines. However, all that needs to be done is to setup one machine, and then duplicate it twice.

> NOTE - For this section, make sure the DC is running so that the client computer can connect to Active Directory

Go to VirtualBox and create a new virtual machine by clicking the 'New' button:

<p align="center">
<img src="../../images/virtualbox_add_vm.jpg" alt="VirtualBox add virtual machine" height="100px">
</p>

Name your virtual machine 'AD-FN-CLIENT1' (Active Directory Domain Controller). This will be the computer for the Finance department.

Select the Windows 10 ISO file for the 'ISO Image' option, and check 'Skip Unattended Installation'. Then click 'Next'.

<p align="center">
<img src="../../images/client_vm_name.png" alt="Client VM name" height="300px">
</p>

For the memory, you can keep it as the default settings, but if you have more resources to use, you can adjust the memory and number of processors in this step and in the future. Click 'Next' when you're happy with the memory.

<p align="center">
<img src="../../images/vbox_mem_allo.png" alt="Allocating memory for VM" height="180px">
</p>

For the virtual hard disk, change it from 50GB to 20GB, as this lab doesn't require a large amount of storage. Then click 'Next'.

<p align="center">
<img src="../../images/vbox_strg_allo.png" alt="Changing hard disk size" height="80px">
</p>

Click 'Finish' on the summary page to create your virtual machine. Then right click your newly created virtual machine and click 'Settings':

<p align="center">
<img src="../../images/vbox_vm_settings_client.png" alt="VM settings button" height="70px">
</p>

Under 'General', click 'Advanced' and change 'Shared Clipboard' and 'Drag'n'Drop' to 'Bidirectonal'. This is to enable clipboard and file sharing between your PC and your virtual machine.

<p align="center">
<img src="../../images/vbox_clipboard_client.png" alt="VM settings button" height="150px">
</p>

Under 'Network', make sure Adapter 1 is attached to 'Internal Network', and choose 'ad-intnet' used by the domain controller. This will connect client VM to the DC's network, allowing it to be used as a AD client computer.

<p align="center">
<img src="../../images/vbox_client_network.png" alt="VM settings button" height="160px">
</p>

Click 'OK'. Your virtual machine is now setup. To start it, click the 'Start' icon or double click the virtual machine.

After some time, the virtual machine will display a setup screen. For the first settings, choose the language, time format, and keyboard settings for you. Then click 'Next'.

<p align="center">
<img src="../../images/win_10_lang_setup.png" alt="Language, time, and keyboard setup Windows Server" height="330px">
</p>

Then click 'Install Now'.

After some time, you will be asked to enter a product key. Click 'I don't have a product key'.

<p align="center">
<img src="../../images/win_10_no_key.png" alt="No product key in Windows 10 setup" height="70px">
</p>

Then select 'Windows 10 Pro' for the operating system and click 'Next'.

<p align="center">
<img src="../../images/win_10_windows_pro.png" alt="Selecting Windows 10 Pro" height="180px">
</p>

Check the box to accept the license terms and click 'Next'. Then select the 'Custom' installation type.

<p align="center">
<img src="../../images/win_10_custom_inst_type.png" alt="Selecting custom Windows installation type" height="120px">
</p>

Click 'Next' and Windows 10 will begin installing.

After some time, the virtual machine will restart automatically and load some more. Eventually, you will be greeted with a screen with options.

> IMPORTANT - This part of the Windows 10 setup includes steps that will differ from instance to instance. This means the steps I outline will differ to the steps you take. The main point though is to make a local user account, which connects to the internal network without unnecessary tracking and ads, so if you set up the client with this in mind, the outcome will be the same.

For the region, make sure your region is selected, and click 'Yes'.

<p align="center">
<img src="../../images/win_10_select_region.png" alt="Selecting region" height="150px">
</p>

For the keyboard layout, make sure your layout is selected, and click 'Yes'.

<p align="center">
<img src="../../images/win_10_select_key.png" alt="Selecting keyboard layout" height="310px">
</p>

Click 'Skip' for the second keyboard layout. After some time, you will be asked how you would like to setup your Windows 10 computer. Select 'Set up for personal use' and click 'Next'.

<p align="center">
<img src="../../images/win_10_personal_setup.png" alt="Selecting personal setup" height="150px">
</p>

Click 'Offline Account' on the bottom right when prompted to add your Microsoft account.

<p align="center">
<img src="../../images/win_10_offline_account.png" alt="Selecting offline account" height="400px">
</p>

Select 'Limited experience' on the bottom right when prompted to sign into Microsoft account.

<p align="center">
<img src="../../images/win_10_limited_exp.png" alt="Selecting limited experience" height="390px">
</p>

Then for the local user's username, make it 'user' and click 'Next'. Leave the password black and click 'Next'.

> NOTE - The user and password will not be used as this will be a computer controlled by Active Directory.

For the browser import prompt, click 'Not now'.

<p align="center">
<img src="../../images/win_10_no_browser_import.png" alt="Selecting not now for browser import" height="390px">
</p>

For the location, ads, and diagnostic data settings, choose either the 'No', 'Limited', or 'Required only' options.

Skip the experience customisation options. Click 'Not now' for Cortana.

Now the account will setup.

<p align="center">
<img src="../../images/win_10_account_setup.png" alt="Windows 10 setting up user account" height="200px">
</p>

After some time, Windows 10 will finally finish setting up, and you will be faced with the main desktop.

<p align="center">
<img src="../../images/win_10_home_screen.png" alt="Windows 10 main desktop" height="400px">
</p>

The next step is to check if the client machine is connected to the AD internal network, and has internet connectivity. Firstly, go to the command prompt by pressing 'START + R', typing in 'cmd' and pressing 'Enter'.


<p align="center">
<img src="../../images/open_cmd.png" alt="Opening command prompt" height="150px">
</p>

Then get the network interface information of the machine:

```cmd
ipconfig
```

The output should look something like this:

<p align="center">
<img src="../../images/ipconfig.png" alt="ipconfig in client machine" height="150px">
</p>

The IPv4 address should be in the ranges specified in the AD DHCP server (172.16.1.100-200), and the default gateway should be the IP address of the DC (172.16.0.1).

To test the internet connectivity, we will send ICMP ping requests to Google.

```cmd
ping www.google.com
```

If the pings are successfully returned to the machine, then the client machine has internet connectivity.

<p align="center">
<img src="../../images/ping_google.png" alt="Pinging Google in client machine" height="150px">
</p>

## Adding Client Machine to Active Directory

Now that the machine has been setup successfully, it needs to be connected to Active Directory.

To do this, right click the Windows icon and select 'System'.

<p align="center">
<img src="../../images/start_system.png" alt="Start > System" height="500px">
</p>

Scroll down and click 'Rename this PC (advanced)'.

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Active Directory Scripting](../active_directory_scripts/)

#### Next Section: [](.)
