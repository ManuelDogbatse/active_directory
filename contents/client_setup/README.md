# Setting Up Client Computer

### Table of Contents

[Setting Up Client Computer Virtual Machine](#setting-up-client-computer-virtual-machine)

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

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Active Directory Scripting](../active_directory_scripts/)

#### Next Section: [](.)
