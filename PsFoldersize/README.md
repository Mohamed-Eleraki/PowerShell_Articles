# PsFoldersize Module

As clear by the author **Mike Roberts** [PsGallery](https://www.powershellgallery.com/packages/PSFolderSize/1.7.1) "This module enables you to gather folder size information, and output the results easily in various ways."

## Install PowerShell core

I'm using Ubuntu distribution, So will go through deb packages, however, if you're using another dist just use The proper package manager.

<details>
<summary><b>Install PowerShell core on Linux</b></summary>

- Download the package "powershell_7.3.4-1.deb_amd64.deb"
  - <https://github.com/PowerShell/PowerShell/releases/tag/v7.3.4>

- set execution permission and Install the package

 ```bash
 chmod +x powershell_7.3.4-1.deb_amd64.deb 
 sudo dpkg -i powershell_7.3.4-1.deb_amd64.deb 
 ```

- Start and print out the Powershell version

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

A module is a package that contains PowerShell members, such as [cmdlets](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7.3), [functions](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.3), [variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_variables?view=powershell-7.3), and [aliases](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_aliases?view=powershell-7.3); in another way Modules is packages contains a list of commands, functions, etc...

<details>
<summary><b>Install PsFoldersize module</b></summary>

 ```bash
 Install-Module -Name PSFolderSize 
 ```

```bash
get-help Get-FolderSize
```

</details>

<details>
<summary><b>Command discovery</b></summary>

 ```bash
 get-help Get-FolderSize -Detailed
 ```

- The tool has powerful capabilities, Let's discover more with  ```get-member```

  ```bash
  Get-FolderSize | gm
  ```

- Any command is an object, and get-member Gets the properties and methods of objects; these methods and properties can be used in advanced tasks. Coming up!

  ```
  PS /home/PowerShellUser> Get-FolderSize | gm

   TypeName: PS.Folder.List.Result

  Name        MemberType   Definition
  ----        ----------   ----------
  Equals      Method       bool Equals(System.Object obj)
  GetHashCode Method       int GetHashCode()
  GetType     Method       type GetType()
  ToString    Method       string ToString()
  FolderName  NoteProperty System.String FolderName=.cache
  FullPath    NoteProperty string FullPath=/home/PowerShellUser/.cache
  HostName    NoteProperty string HostName=
  SizeBytes   NoteProperty double SizeBytes=435597898
  SizeGB      NoteProperty double SizeGB=0.41
  SizeKB      NoteProperty double SizeKB=425388.57
  SizeMB      NoteProperty double SizeMB=415.42 ```

- ***TypeName***: means that the listed members provide more result capabilities, More explanation coming up!
  - ***Another example***: ```get-process``` what out-put do you expect from this command!? for sure ***processes***, So the members of```get-process``` command provide more capabilites at the process out-put, So ```Get-FolderSize``` **Members** provide more **Result capabilites** out-put.

- ***MemberType***:
  - ***method***: Things I can do.
  - ***NoteProperties***: generic properties.
  - ***properties***: >> Things I have, Things that describe me (e.g. my skin color, my eyes color, etc...)

- **Exmples**:

```bash
cd ~
Get-FolderSize     

FolderName                     SizeMB       SizeGB       FullPath
----------                     ------       ------       --------
Downloads                      152.86       0.15         /home/PowerShellUser/Downloads

```

```bash
# Print out folder name only
Get-FolderSize | select -Property FolderName

FolderName
----------

Downloads

```

```bash
# Print out folder name and size
Get-FolderSize | select -Property FolderName, SizeGB

FolderName   SizeGB
----------   ------

Downloads     0.150

```

```bash
# Print out full path and size
Get-FolderSize | select -Property FullPath, SizeGB  

FullPath                                SizeGB
--------                                ------
/home/PowerShellUser/Downloads           0.150

```

```bash
# Filtter the out-put with sizeGB that equal 0.15  
Get-FolderSize | Where-Object SizeGB -eq 0.15

FolderName                     SizeMB       SizeGB       FullPath
----------                     ------       ------       --------
Downloads                      152.86       0.15         /home/PowerShellUser/Downloads

```

```bash
# Filtter the out-put with sizeGB that match "0.anySize"
Get-FolderSize | Where-Object SizeGB -match "0.1*"

FolderName                     SizeMB       SizeGB       FullPath
----------                     ------       ------       --------

Downloads                      152.86       0.15         /home/PowerShellUser/Downloads
.config                        60.91        0.06         /home/PowerShellUser/.config

```

- [MATCH about_Comparison_Operators](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.2)

```bash
# Filter the out-put with size criteria and select only full path out-put, and set it in a variable, Then you can use this variable to copy the items, looping, ifcondetions, etc
$getFolderSize = Get-FolderSize | Where-Object SizeGB -eq 0.15 | select -Property fullpath
```

**get-help Examples**:

```bash
# The default format out-put is Table however, there's a list as well  
# select the format output as "table" with "autosize" option to ignore hidden values 
Get-FolderSize | Format-Table -AutoSize
```

```bash
# specify a path
Get-FolderSize -BasePath 'C:\Program Files'
```

```bash
# Spicify a path and the exact folder name
Get-FolderSize -BasePath 'C:\Program Files' -FolderName IIS
```

```bash
# define a variable called $getFolderSize have folder size data, And Reuse the variable with table format 
$getFolderSize = Get-FolderSize 
$getFolderSize | Format-Table -AutoSize
```

```bash
# define a variable called $getFolderSize that has folder size data and save the value in ~/Desktop path with csv extension
$getFolderSize = Get-FolderSize -Output csv -OutputPath ~\Desktop
$getFolderSize

```

```bash
# sort by size descending
Get-FolderSize | Sort-Object SizeBytes -Descending
```

```bash
# Use Omitfolders option to exclude pictures folder out-put
Get-FolderSize -OmitFolders ./Pictures/
```

</details>
