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

> NOTE - The user and password will not be used as this will be a computer controlled by Active Directory. However, in a production environment, use a stronger username and password.

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

Before adding the PC to Active Directory, add VirtualBox to improve the display. Click Devices > Insert Guest Additions CD image in the toolbar on the top left of the virtual machine window.

<p align="center">
<img src="../../images/insert_guest_add.png" alt="Inserting Guest Additions CD image" height="230px">
</p>

Then inside the VM, open File Explorer and go to This PC > CD Drive (D:) VirtualBox Guest Additions. Then click the Windows executable ending in 'amd64' to open the Guest Additions installer:

<p align="center">
<img src="../../images/amd-64-exe.png" alt="Guest Additions Executable" height="100px">
</p>

Click Next > Next > Install to install Guest Additions. After it installs, select the 'I want to manually reboot later' option and click Finish.

<p align="center">
<img src="../../images/guest_add_finish.png" alt="Finishing Guest Additions Installation" height="300px">
</p>

Then manually shut down the computer and reopen it for Guest Additions to take effect.

Before moving onto the next step, take a snapshot of the client VM's current state, as this will be used as a base template for the other client VMs.

To do this, make sure the client VM is shut down, then in VirtualBox, click the slider icon on the right of the virtual machine, and click 'Snapshots'.

<p align="center">
<img src="../../images/snapshot_option.png" alt="VirtualBox snapshot option" height="90px">
</p>

Then click the 'Take' icon to take a snapshot. Give the snapshot the name 'AD-CLIENT Base State' and click 'OK' to create the snapshot.

<p align="center">
<img src="../../images/created_snapshot.png" alt="Created new snapshot" height="130px">
</p>

Now that the base snapshot has been taken, clone the snapshot by clicking on the snapshot, and clicking the 'Clone' icon.

<p align="center">
<img src="../../images/clone_option.png" alt="Clone state icon" height="110px">
</p>

Change the name to 'AD-HR-CLIENT1', and make sure that the MAC address policy is not 'Include all network adapter MAC addresses'. This will result in the two client machines having the same MAC address and as a result, using the same IP address in AD. Then click 'Next'.

<p align="center">
<img src="../../images/clone_name.png" alt="Renaming clone VM" height="200px">
</p>

Make sure that 'Full clone' is selected and then click 'Next'. Then make sure 'Current machine state' is selected and the click 'Finish'. After some time, you will now have a clone of the first client machine.

Repeat the cloning process again, but this time create a clone named 'AD-IT-CLIENT1' for the IT department client computer.

<p align="center">
<img src="../../images/client_vm_list.png" alt="Client VM list" height="200px">
</p>

## Adding Client Machine to Active Directory

Now that the machine has been setup successfully, it needs to be connected to Active Directory.

To do this, right click the Windows icon and select 'System'.

<p align="center">
<img src="../../images/start_system.png" alt="Start > System" height="500px">
</p>

Scroll down and click 'Rename this PC (advanced)'. If it's not at the bottom of the page, then it should be on the right of the page.

<p align="center">
<img src="../../images/win_10_rename_pc.png" alt="Rename PC" height="70px">
</p>

Then click 'Change'.

<p align="center">
<img src="../../images/change_name.png" alt="Change name of PC" height="50px">
</p>

Name the PC the same name as the computer object within Active Directory. In this case 'FN-CLIENT1'. Click the 'Domain' radio button and type 'mydomain.com' into the domain name. Then click 'OK'.

<p align="center">
<img src="../../images/renaming_client.png" alt="Changing name of PC to AD computer name" height="300px">
</p>

A popup will appear asking you to enter the account details of an account in the AD domain. Use the custom administrator account's username and password and click 'OK'.

<p align="center">
<img src="../../images/admin_login_for_client.png" alt="Adding the admin's details to connect the PC to AD" height="150px">
</p>

If successful, you will be given a popup welcoming your PC to 'mydomain.com'. Click 'OK > OK' and then close the PC name settings to get the restart prompt. Select 'Restart Now' to restart your computer.

<p align="center">
<img src="../../images/restart_client.png" alt="Restarting the client computer" height="160px">
</p>

After resetting the computer, click 'Other User' on the bottom right of the login screen.

<p align="center">
<img src="../../images/other_user_client.png" alt="Other user" height="120px">
</p>

You will now see that you can login as a user from 'MYDOMAIN'. For this example, we will use the first Finance user, which is 'aabrev'. Enter the login credentials for 'aabrev' and press Enter to login.

<p align="center">
<img src="../../images/ad_login_client.png" alt="Signing into client as AD user" height="350px">
</p>

After logging in, wait for a minute and after the account has been set up, the AD user will be successfully logged in through the client PC.

Repeat the process of renaming the PC for the other two client machines. Make sure to rename the PC to 'HR-CLIENT1' for the HR VM, and 'IT-CLIENT1' for the IT VM.

To see the changes, go to the DC and go to the DHCP tool. If you go to the address leases in you defined scope, you will see the client PCs.

<p align="center">
<img src="../../images/clients_in_dhcp.png" alt="Client computer in DHCP" height="90px">
</p>

Also, if you go to 'Active Directory Users and Computers' and click the properties of the client PC connected to AD, it will show you the operating system of the client PC in its properties.

<p align="center">
<img src="../../images/client_in_users_and_comps.png" alt="Client computer in Users and Computers" height="170px">
</p>

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Active Directory Scripting](../active_directory_scripts/)

#### Next Section: [](.)
