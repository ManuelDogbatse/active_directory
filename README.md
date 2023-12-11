# Administering Windows Accounts in a Private Network using Active Directory

## Introduction

In this project, I set up a basic home lab environment where I configured Active Directory on a domain controller running Windows Server 2019 on a virtual machine using VirtualBox. I then made a Powershell script that added 1000+ users and created 3 organisational units to simulate 3 typical departments a company would have. I then added group policies to each department and added file sharing permissions to implement the principle of least privilige.

## Requirements

For this project, you need VirtualBox installed, as well as the ISO files for both Windows 10 and Windows Server 2019. No specific hardware or OS is required, but the lab performs the best on computers with a good amount of memory and CPU (≥ 8GB RAM and ≥ 8 core processor).

## Sections

> NOTE - Files created in this project can be found in the directory of the section they have been created in

### [Setting up Virtual Machines](./contents/virtual_machine_setup/)

Setting up virtual machines for Active Directory lab
