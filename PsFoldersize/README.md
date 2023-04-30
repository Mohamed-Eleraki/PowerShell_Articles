# PsFoldersize Module


As cleaify by the author **Mike Roberts** "This module enables you to gather folder size information, and output the results easily in various ways."
## Install PowerShell core

i'm using Ubunto destrubution, So will going through deb packages, however if you're using another dest just use The proper package manager.

<details>
<summary>Install PowerShell core on Linux </summary>


 - Download the package "powershell_7.3.4-1.deb_amd64.deb"
   - https://github.com/PowerShell/PowerShell/releases/tag/v7.3.4
 - set execution permission and Install the package

	```bash
	chmod +x powershell_7.3.4-1.deb_amd64.deb 
	sudo dpkg -i powershell_7.3.4-1.deb_amd64.deb 
	```
 - Start and print out Powershell version

	```bash
	pwsh
	```
	```bash
	$PSVersionTable
	```

- The output should be like that:

	```bash
	Name                           Value
	----                           -----
	PSVersion                      7.3.4
	PSEdition                      Core
	GitCommitId                    7.3.4
	OS                             Linux 5.15.0-71-generic
	Platform                       Unix
	PSCompatibleVersions           {1.0}
	PSRemotingProtocolVersion      2.3
	SerializationVersion           1.1.0.1
	WSManStackVersion              3.0

	```



</details>


## Install PsFoldersize module

A module is a package that contains PowerShell members, such as [cmdlets](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7.3), [functions](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.3), [variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_variables?view=powershell-7.3), and [aliases](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_aliases?view=powershell-7.3); in another way Modules is packages contains list of commands, function, etc...

<details>
<summary>Install PsFoldersize module</summary>

 - Print-out the existing modules

</details>