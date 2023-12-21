# Setting up Active Directory Domain Services

### Table of Contents

[Setting up Network Interfaces](#setting-up-network-interfaces)

[Sections](#sections)

## Setting up Network Interfaces

Before installing Active Directory onto the DC, the networks need to be configured, as well as the hostname for the DC.

To see the network adapter settings, click the network icon on the right of the taskbar.

<p align="center">
<img src="../../images/network_button.png" alt="Network Icon in Taskbar" height="100px">
</p>

Then select 'Network & Internet Settings'. Then select the 'Ethernet' tab and select 'Change adapter options' on the right hand side of the window. You will now see the two network interfaces defined when creating the virtual machine.

<p align="center">
<img src="../../images/network_interfaces.png" alt="Network interface list" height="50px">
</p>

Since both have the same name, you must first differentiate the NAT interface from the internal network interface. One way to know is that the NAT interface will be connected to the internet, and say 'Network', whereas the internal network will say 'Unidentified network'. To confirm this, right click each interface and select Status > Details.

<p align="center">
<img src="../../images/network_interface_details.png" alt="Network connection details" height="350px">
</p>

For the NAT network, the IPv4 address will be '10.0.x.x' address and will have an IPv4 Default Gateway. For the internal network, the IPv4 address will be '169.254.x.x' and will not have a default gateway.

After differentiating the NAT interface from the internal network interface, rename them by right clicking, then selecting 'Rename'. Change the NAT interface to 'O_Internet_O' and change the internal network interface to 'X_Internal_X'.

Then change the settings for the internal network interface. Right click it and select 'Properties'. Then click 'Internet Protocol Version 4 (TCP/IPv4)'.

<p align="center">
<img src="../../images/ipv4_option.png" alt="IPv4 option" height="30px">
</p>

Select the 'Use the following IP address' option and enter the IP address, subnet mask and DNS server from [the diagram](../../README.md/#design) outlined in the project design.

<p align="center">
<img src="../../images/ipv4_settings.png" alt="Custom IPv4 settings" height="240px">
</p>

Then click OK > OK and close the Control Panel and Settings window.

To change the computer's hostname, right click the Start button and select 'System'. Then click 'Rename this PC'.

<p align="center">
<img src="../../images/rename_pc.png" alt="Rename PC option" height="220px">
</p>

Change the name to 'DC' and click 'Next', then click 'Restart Now > Continue' to restart the DC computer.

<p align="center">
<img src="../../images/rename_pc_to_dc.png" alt="Renaming PC to DC" height="200px">
</p>

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Setting up Virtual Machines](../virtual_machine_setup/)

#### Next Section: [...](.)
