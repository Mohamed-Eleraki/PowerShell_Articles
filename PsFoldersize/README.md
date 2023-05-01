# PsFoldersize Module

As cleaify by the author **Mike Roberts** "This module enables you to gather folder size information, and output the results easily in various ways."

## Install PowerShell core

i'm using Ubunto destrubution, So will going through deb packages, however if you're using another dest just use The proper package manager.

<details>
<summary>Install PowerShell core on Linux </summary>

- Download the package "powershell_7.3.4-1.deb_amd64.deb"
  - <https://github.com/PowerShell/PowerShell/releases/tag/v7.3.4>
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

- Install PsFoldersize

 ```bash
 Install-Module -Name PSFolderSize 
 ```

- Discover tool usage

 ```bash
 get-help Get-FolderSize -Detailed
 ```

- The tool have a powerfull cabapilities, Let's dicover the command members

  ```bash
  Get-FolderSize | gm
  ```

- gm = get-member, any command is an object, and get-member Gets the properties and methods of objects; these methods and properties can be use in advanced tasks

- The out-put

  ```bash

      TypeName: PS.Folder.List.Result

  Name        MemberType   Definition
  ----        ----------   ----------
  Equals      Method       bool Equals(System.Object obj)
  GetHashCode Method       int GetHashCode()
  GetType     Method       type GetType()
  ToString    Method       string ToString()
  FolderName  NoteProperty System.String FolderName=.thunderbird
  FullPath    NoteProperty string FullPath=/home/mohamed/.thunderbird
  HostName    NoteProperty string HostName=ThinkPad
  SizeBytes   NoteProperty double SizeBytes=387109585
  SizeGB      NoteProperty double SizeGB=0.36
  SizeKB      NoteProperty double SizeKB=378036.7
  SizeMB      NoteProperty double SizeMB=369.18

  ```

- These member working as Result
- properties >> things I have Things that describe me
- methoods thing I can do
- TypeName: PS.Folder.List.Result what is the object send me is send me a result, take get-process for example it's send me a process.

</details>
