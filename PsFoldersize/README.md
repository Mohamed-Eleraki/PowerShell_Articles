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

## PsFoldersize module

A module is a package that contains PowerShell members, such as [cmdlets](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7.3), [functions](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.3), [variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_variables?view=powershell-7.3), and [aliases](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_aliases?view=powershell-7.3); in another way Modules is packages contains list of commands, function, etc...

<details>
<summary>Install PsFoldersize module</summary>

- Install PsFoldersize

 ```bash
 Install-Module -Name PSFolderSize 
 ```

```bash
get-help Get-FolderSize
```

</details>

<details>
<summary>Discovering The Command!</summary>

 ```bash
 get-help Get-FolderSize -Detailed
 ```

- The tool have a powerfull cabapilities, Let's dicover more with ```get-member```

  ```bash
  Get-FolderSize | gm
  ```

- Any command is an object, and get-member Gets the properties and methods of objects; these methods and properties can be use in advanced tasks. Coming up!

  ```
  PS /home/mohamed> Get-FolderSize | gm

   TypeName: PS.Folder.List.Result

  Name        MemberType   Definition
  ----        ----------   ----------
  Equals      Method       bool Equals(System.Object obj)
  GetHashCode Method       int GetHashCode()
  GetType     Method       type GetType()
  ToString    Method       string ToString()
  FolderName  NoteProperty System.String FolderName=.cache
  FullPath    NoteProperty string FullPath=/home/mohamed/.cache
  HostName    NoteProperty string HostName=ThinkPad
  SizeBytes   NoteProperty double SizeBytes=435597898
  SizeGB      NoteProperty double SizeGB=0.41
  SizeKB      NoteProperty double SizeKB=425388.57
  SizeMB      NoteProperty double SizeMB=415.42 ```

- Now Let's discover The out-put:
  - ***TypeName***: means that the listed members provide more result capabilites, More explination coming up!
    - ***Another example***: ```get-process``` what out-put do you expect from this command!? for sure ***processes***, So the members of```get-process``` command provide more capabilites at the process out-put.

  - ***MemberType***:
    - ***method***: Things I can do.
    - ***NoteProperties***: generic properties.
    - ***properties***: >> Things I have, Things that describe me.

</details>
