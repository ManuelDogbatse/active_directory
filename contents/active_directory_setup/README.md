# Setting up Active Directory Domain Services

### Table of Contents

[Setting up Network Interfaces](#setting-up-network-interfaces)

[Installing Active Directory](#installing-active-directory)

[Adding New Administrator User](#adding-new-administrator-user)

[Setting up NAT for Internet Access](#setting-up-nat-for-internet-access)

[Setting up DHCP server](#setting-up-dhcp-server)

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

Now your DC VM will have the hostname 'DC'.

## Installing Active Directory

To install Active Directory Domain Services to the DC, go to the server manager application, which by default will display its dashboard.

<p align="center">
<img src="../../images/server_manager_dashboard.png" alt="Server Manager dashboard" height="400px">
</p>

Click on 'Add roles and features' to add Active Directory. Click 'Next > Next'. For the server selection, you should see the DC server with the configured IP addresses.

<p align="center">
<img src="../../images/server_selection.png" alt="Server Selection" height="65px">
</p>

Click Next. Then select the 'Active Directory Domain Services' checkbox. Then click 'Add Features' in the popup. Then click 'Next > Next > Next > Install' to install Active Directory Domain Services.

Once the blue bar fills up, the installation is complete. Click 'Close', and then click the flag with the warning symbol on the top right of the Server Manager dashboard.

<p align="center">
<img src="../../images/server_manager_flag.png" alt="Server Manager flag" height="270px">
</p>

Click 'Promote this server to a domain controller' to make the virtual machine the DC for your Active Directory lab.

Under 'Deployment Configuration' select the 'Add a new forest' option and enter 'mydomain.com' as the root domain name of the Active Directory network. Then click 'Next'.

<p align="center">
<img src="../../images/set_domain_name.png" alt="Setting domain name for AD" height="150px">
</p>

Then enter a password in the DSRM field. Then click 'Next'.

<p align="center">
<img src="../../images/dsrm_password.png" alt="Setting password for DSRM" height="90px">
</p>

Click 'Next > Next > Next > Next > Next > Install'. When the installation is complete, a popup will appear. Click 'Close' and then click 'Close' in the installation window to automatically restart the VM.

Now when you log in, the administrator account will have 'MYDOMAIN\' prepended to it.

<p align="center">
<img src="../../images/new_login.png" alt="New login for DC" height="270px">
</p>

## Adding New Administrator User

In system administration, it is good practice to create users with administration privileges to perform administration tasks, rather than using the default administrator account.

To do this, go to the Start Menu > Windows Administrative Tools > Active Directory Users and Computers.

<p align="center">
<img src="../../images//start_menu_users.png" alt="Users and Computers via Start Menu" height="220px">
</p>

Alternatively, on the Server Manager dashboard, click 'Tools' in the top right of the window, and select 'Active Directory Users and Computers'.

<p align="center">
<img src="../../images/ser_man_dash_users.png" alt="Users and Computers via Server Manager Dashboard" height="150px">
</p>

Expand the 'mydomain.com' directory on the left of the window.

<p align="center">
<img src="../../images/users_and_comps_mydomain.png" alt="mydomain.com inside Users and Computers" height="130px">
</p>

Then right click 'mydomain.com' and select New > Organisational Unit. An organisational unit (OU) is a directory for storing different objects in Active Directory, such as users, computers, and groups.

Name this OU '\_Admins'. Prepending underscores to OUs makes it easier to identify custom OUs in large quantities.

<p align="center">
<img src="../../images/create_new_ou.png" alt="mydomain.com inside Users and Computers" height="300px">
</p>

> NOTE - If you want to experiment with OUs, uncheck 'Protect container from accidental deletion' to allow the deletion of the OU without extra steps.

Click 'OK' to create the admin OU. Then right click the newly created OU and select New > User. Enter a first name and a surname, then for the user logon name, name it 'a-' followed by the initial of the first name and the full surname e.g. for John Doe: 'a-jdoe'. Then click 'Next'.

<p align="center">
<img src="../../images/creating_user.png" alt="Creating a new user" height="300px">
</p>

Enter a password for the user, and for this lab, uncheck 'User must change password on next logon' and check 'Password never expires'.

> NOTE - In the real world, keep 'User must change password on next logon' checked and 'Password never expires' unchecked for extra security.

<p align="center">
<img src="../../images/creating_user_password.png" alt="Creating password for the new user" height="300px">
</p>

Click 'Next > Finish' to create the user.

Then to give the user administrator privileges, right click the user, and select 'Properties'. Then go to the 'Member Of' tab and click 'Add'.

<p align="center">
<img src="../../images/add_user_to_group.png" alt="Adding user to group" height="250px">
</p>

Search 'domain admins' and click 'Check Names' to resolve the search. Then click 'OK'.

<p align="center">
<img src="../../images/search_for_group.png" alt="Searching for a group name" height="80px">
</p>

Then click 'Apply' and then 'OK' in the properties window to confirm the change. Now the user has been added to the domain admins group and has administrator privileges.

Then sign out and login as the newly created admin user. To do this, on the login screen, click 'Other User' on the bottom left of the screen.

<p align="center">
<img src="../../images/other_user.png" alt="Other user tab in login screen" height="110px">
</p>

Enter the logon name of the admin user and their password, and press 'Enter'.

<p align="center">
<img src="../../images/new_user_login.png" alt="Logging in as the new user" height="350px">
</p>

You will now login as the admin user.

## Setting up NAT for Internet Access

Remote Access is a service in Active Directory, which has Network Access Translation (NAT) capabilities. NAT allows the client computers to access the internet by using the domain controller's public IP address, which is provided by the domain controller's NAT network adapter in VirtualBox.

> NOTE - This setup is not suitable in a production environment. The best setup for internet access is to make the router the default gateway for both the DC and client computers, and set the DC as the DNS server for the client computers.

To download Remote Access, go to Server Manager and click 'Add roles and features'. On the window, click 'Next > Next > Next'. Select 'Remote Access' and click 'Next > Next > Next'.

<p align="center">
<img src="../../images/remote_access_option.png" alt="Remote Access option" height="80px">
</p>

For the Remote Access roles, select 'Routing'.

<p align="center">
<img src="../../images/routing_option.png" alt="Routing option" height="60px">
</p>

On the popup, click 'Add Features', then click 'Next > Next > Next > Install'.

Once the installation is complete, click 'Close' and go to 'Tools' on the top right of the Server Manager and click 'Routing and Remote Access'.

<p align="center">
<img src="../../images/routing_and_remote_access.png" alt="Routing and Remote Access" height="70px">
</p>

In the new window, right click 'DC (local)', and select 'Configure and Enable Routing and Remote Access'. In the setup wizard, click 'Next' and select the 'NAT' radio button. Then click 'Next'.

<p align="center">
<img src="../../images/select_nat.png" alt="Selecting NAT option" height="200px">
</p>

Then from the two network interfaces that show up, select the internet one, which in this lab is named 'O_Internet_O'.

<p align="center">
<img src="../../images/internet_interface_select.png" alt="Selecting internet interface" height="120px">
</p>

> NOTE - If the interfaces do not show up, close the setup wizard and Routing and Remote Access, and reopen them.

Click 'Next > Finish', and the NAT will begin to setup.

> NOTE - If you get the following warning after clicking 'Finish', press OK and the NAT will setup anyway.
>
> <p align="center">
> <img src="../../images/nat_warning.png" alt="NAT setup warning" height="180px">
> </p>

Once the NAT has been setup, the 'DC (local)' text in the Routing and Remote Access window has changed from a circle with a red arrow to a circle with a green arrow. This means the NAT has been setup successfully.

<p align="center">
<img src="../../images/green_dc_local.png" alt="DC local icon changes to green arrow" height="25px">
</p>

## Setting up DHCP server

Active Directory has a DHCP server feature, which automatically leases IP addresses to client devices connected to the internal network, giving them the ability to communicate with each other and the internet.

To install the DHCP service, go to Server Manager, and select 'Add roles and features' and click 'Next > Next > Next'. Now select 'DHCP Server' and click 'Add Features' in the popup window.

<p align="center">
<img src="../../images/dhcp_server_option.png" alt="DHCP server option" height="55px">
</p>

Then click 'Next > Next > Next > Install' to install the DHCP service. Once the installation is complete, click 'Close'. Then on Server Manager, go to 'Tools > DHCP'.

On the left, click the arrow next to  your domain controller's domain name (dc.mydomain.com), right click 'IPv4' and select 'New Scope'.

<p align="center">
<img src="../../images/dhcp_new_scope.png" alt="DHCP new scope" height="110px">
</p>

Click 'Next', then give the scope the name '172.16.0.100-200' and click 'Next'.

<p align="center">
<img src="../../images/dhcp_scope_name.png" alt="Creating DHCP scope name" height="80px">
</p>

Add the '172.16.0.100' as the start IP address, '172.16.0.200' as the end IP address, and 24 for the length, which will automatically make the subnet mask '255.255.255.0'.

<p align="center">
<img src="../../images/dhcp_ranges.png" alt="Setting up DHCP scope" height="250px">
</p>

Click 'Next > Next'. For the lease duration, it is set as 8 days by default, which is a sensible value. This should be decreased if this was a DHCP server for a public WiFi network. Click 'Next'.

<p align="center">
<img src="../../images/dhcp_lease_time.png" alt="DHCP lease times" height="70px">
</p>

Make sure that 'Yes' is selected in the configure DHCP options page and click 'Next'.

<p align="center">
<img src="../../images/configure_dhcp.png" alt="Configure DHCP options" height="80px">
</p>

For the default gateway, type '172.16.0.1', which is the IP address of the DC. Then click 'Add' and select the IP address. Then click 'Next'.

<p align="center">
<img src="../../images/dhcp_default_gateway.png" alt="Setting DHCP default gateway" height="180px">
</p>

For the DNS server, select the IP address of the DC and then click 'Next'.

<p align="center">
<img src="../../images/dhcp_dns_server.png" alt="Setting DHCP DNS server" height="200px">
</p>

Click 'Next > Next > Finish' to complete the DHCP scope setup. On the DHCP window, right click the DC domain name and click 'Authorize'.

<p align="center">
<img src="../../images/authorise_dhcp_server.png" alt="Authorising DHCP server" height="100px">
</p>

Then right click the DC domain name again and click 'Refresh'. Now the IPv4 and IPv6 text will have green tick icons. This means DHCP has been setup successfully.

<p align="center">
<img src="../../images/dhcp_success.png" alt="Successfully setup DHCP server" height="60px">
</p>

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Setting up Virtual Machines](../virtual_machine_setup/)

#### Next Section: [Active Directory Scripting](../active_directory_scripts/)
