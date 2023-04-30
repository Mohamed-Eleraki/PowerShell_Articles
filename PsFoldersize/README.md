# PsFoldersize Module


As cleaify by the author **Mike Roberts** "This module enables you to gather folder size information, and output the results easily in various ways."
## install PowerShell core

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
 - Run and print out Powershell version

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
	OS                             Linux 5.15.0-71-generic #78~20.04.1-Ubuntu SMP Wed Apr 19 11:26:48 UTC 2023
	Platform                       Unix
	PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0…}
	PSRemotingProtocolVersion      2.3
	SerializationVersion           1.1.0.1
	WSManStackVersion              3.0

	```



</details>