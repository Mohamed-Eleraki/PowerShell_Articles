# PowerShell Profiles

<details>
<summary><b>Problems solved</b></summary>

- **Senario 01:** You are usnig PowerShell to create bunch of AD users from excel sheet, Using script like the below:

  ```bash
    # This script for clearification only, and not tested! 
    ​import-csv -path c:\temp\users.csv | foreach {

    $givenName = $_.name.split()[0] 
    $surname = $_.name.split()[1]
    new-aduser -name $_.name -enabled $true –givenName $givenName –surname $surname -accountpassword (convertto-securestring $_.password -asplaintext -force) -changepasswordatlogon $true -samaccountname $_.samaccountname –userprincipalname ($_.samaccountname+”@ad.contoso.com”) -city $_.city -department $_.department
    }

  ```
  
  Each time you'll go and open-up your script and edit the ```import-csv``` path to refer to the new excel sheet you want to woke on. These steps are a little overwhelming. Instead you can define this script as a function in powershell profile and parameterize the ```import-csv``` path, So each time to create bunch of users just open the PowerSell terminal and type the name of function and send the new path of your excel sheet as an option!!

- **Senario 02:** You have multiple scripts in your environment, and you have some variables and functinos that you're using continuously in each script, So you're defining in each script the same variables and functions, etc. in short period you'll find out that your script become more complix; To make the script simple in as posible you can define all those variables and function in PowerShell profile and just recall it in your script.

</details>

<p>
You can create a PowerShell profile to customize your environment, You can add commands, aliases, functions, variables, modules, PowerShell drives and more. You can also add other session-specific elements to your profile so they're available in every session without having to import or re-create them. A PowerShell profile is a script that runs when PowerShell starts. You can have multiple profiles per user or host, The Host here is for powershell itself not for the machine, and if you want to navigating on machines with the same profile you can use onedrive instead.
</p>

  <p>
    These PowerShell Profiles are stored as files, You can have several profile files, and you can even have profiles that are specific to a particular host. Here the basic profile file paths:
  </p>

  ```bash  
    PS /home/mohamed> $PROFILE.CurrentUserCurrentHost
    /home/mohamed/.config/powershell/Microsoft.PowerShell_profile.ps1
  ```
  

  
  ```bash  
    PS /home/mohamed> $PROFILE.CurrentUserAllHosts   
    /home/mohamed/.config/powershell/profile.ps1
  ```
  

  
  ```bash  
    PS /home/mohamed> $PROFILE.AllUsersCurrentHost                                  
    /opt/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
  ```
 

  
  ```bash  
    PS /home/mohamed> $PROFILE.AllUsersAllHosts   
    /opt/microsoft/powershell/7/profile.ps1
  ```
  

*Here I'm using PowerShell core on Linux, you can use PS on WIN as well, however if you want to install the PowerShell Liunx version follow this article: [Install PowerShell core](https://github.com/Mohamed-Eleraki/PowerShell_Articles/tree/main/PsFoldersize#install-powershell-core)*

These Paths are stored under there main Directory "/home/user" and "/opt/microsoft/powershell/7"  you can call them using the variables as well:

```bash
  PS /home/mohamed> $home                    
  /home/mohamed
```

```bash
  PS /home/mohamed> $PSHOME                     
  /opt/microsoft/powershell/7
```

The CurrentUserCurrentHost ```$PROFILE.CurrentUserCurrentHost``` is known as your powershell profile.

To view all the current properties of $profile, use the following command:
```bash
  PS /home/mohamed> $PROFILE | Get-Member -Type NoteProperty | ft -AutoSize

     TypeName: System.String

  Name                   MemberType   Definition
  ----                   ----------   ----------
  AllUsersAllHosts       NoteProperty string AllUsersAllHosts=/opt/microsoft/powershell/7/profile.ps1
  AllUsersCurrentHost    NoteProperty string AllUsersCurrentHost=/opt/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
  CurrentUserAllHosts    NoteProperty string CurrentUserAllHosts=/home/mohamed/.config/powershell/profile.ps1
  CurrentUserCurrentHost NoteProperty string CurrentUserCurrentHost=/home/mohamed/.config/powershell/Microsoft.PowerShell_profile.ps1
```
To view all the current Members, use the following command:

```bash
  PS /home/mohamed> $PROFILE | gm | ft -AutoSize                           

     TypeName: System.String

  Name                   MemberType            Definition
  ----                   ----------            ----------
  Clone                  Method                System.Object Clone(), System.Object ICloneable.Clone()
  CompareTo              Method                int CompareTo(System.Object value), int CompareTo(string strB), int IComparable.CompareTo(Syste…
  Contains               Method                bool Contains(string value), bool Contains(string value, System.StringComparison comparisonType…
  CopyTo                 Method                void CopyTo(int sourceIndex, char[] destination, int destinationIndex, int count), void CopyTo(…
  EndsWith               Method                bool EndsWith(string value), bool EndsWith(string value, System.StringComparison comparisonType…
  EnumerateRunes         Method                System.Text.StringRuneEnumerator EnumerateRunes()
  .
  .
  .

```