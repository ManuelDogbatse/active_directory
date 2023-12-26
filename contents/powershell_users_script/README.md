# Creating Users using Powershell Script

### Table of Contents

[Powershell Script](#powershell-script)

[Sections](#sections)

## Powershell Script

Now that Active Directory has been setup, it is time to simulate a real-world example of Active Directory in use to manage a company's users and computers. Creating objects in Active Directory can be automated through the use of Powershell scripts, with the use of the Active Directory API.

I have written two scripts: one in Python, and one in Powershell. The Python script is responsible for reformatting the names text file to ensure that no empty lines are added as AD users, and that there are no duplicate usernames from clashing first name initials and surname combinations. The Powershell script creates organisational units for each department in the departments text file, and then creates users using the formatted names text file and adds them to one of the three departments using a loop.

To run these scripts, firstly

## Sections

#### Home Page: [Active Directory](../../)

#### Previous Section: [Setting up Active Directory Domain Services](../active_directory_setup/)

#### Next Section: [](.)