# PowerShell Profiles

<details>
<summary><b>Problems solved</b></summary>

- **Senario 01:** You are usnig PowerShell to create **bunch of AD users** from excel sheet, Using script like the below:

  ```bash
    # This script for clearification only, and not tested! 
    ​import-csv -path c:\temp\users.csv | foreach {

    $givenName = $_.name.split()[0] 
    $surname = $_.name.split()[1]
    new-aduser -name $_.name -enabled $true –givenName $givenName –surname $surname -accountpassword (convertto-securestring $_.password -asplaintext -force) -changepasswordatlogon $true -samaccountname $_.samaccountname –userprincipalname ($_.samaccountname+”@ad.contoso.com”) -city $_.city -department $_.department
    }

  ```
  
  Each time you'll go and open-up your script and edit the ```import-csv``` path to refer to the new excel sheet you want to woke on. These steps are a little overwhelming. **Instead**, you can define this script as a **function** in powershell profile and **parameterize** the ```import-csv``` path, So each time to create a bunch of users just open the **PowerSell terminal** and type the name of the function and **pass** the new path of your excel sheet as an option, Traa!!

- **Senario 02:** You have **multiple scripts** in your environment, and you have some variables and functions that you're **using continuously** in each script, So you're defining in each scripts **the same variables and functions, etc.** in short period you'll find out that your script become more **complex;** To make the script simple in as possible you can define all those variables and function in **PowerShell profile** and just **recall** them in your script.

</details>


You can create a **PowerShell profile** to **customize your environment**, You can add commands, aliases, functions, variables, modules, PowerShell drives and more. You can also add other session-specific elements to your profile so they're available in every session without having to import or re-create them. **A PowerShell profile** is a script that runs when **PowerShell starts**. You can have **multiple profiles** per user or host, The Host here is for powershell itself not for the machine, and if you want to navigate on machines with the same profile you can use **onedrive** instead.


  
  These **PowerShell Profiles** are stored as files, You can have **several profile files**, and you can even have profiles that are specific to a particular host. Here the basic **profile file paths:**
  

  ```bash  
    PS /home/Ps_user> $PROFILE.CurrentUserCurrentHost
    /home/Ps_user/.config/powershell/Microsoft.PowerShell_profile.ps1
  ```
  

  
  ```bash  
    PS /home/Ps_user> $PROFILE.CurrentUserAllHosts   
    /home/Ps_user/.config/powershell/profile.ps1
  ```
  

  
  ```bash  
    PS /home/Ps_user> $PROFILE.AllUsersCurrentHost                                  
    /opt/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
  ```
 

  
  ```bash  
    PS /home/Ps_user> $PROFILE.AllUsersAllHosts   
    /opt/microsoft/powershell/7/profile.ps1
  ```
  

*In this lab I'm using PowerShell core on Linux, you can use PS on WIN as well, however if you want to install the PowerShell Linux version follow this article: [Install PowerShell core](https://github.com/Ps_user-Eleraki/PowerShell_Articles/tree/main/PsFoldersize#install-powershell-core)*

These **Paths** are stored under **their main Directory** "/home/user" and "/opt/microsoft/powershell/7"  you can call them using the **variables** as well:

```bash
  PS /home/Ps_user> $home                    
  /home/Ps_user
```

```bash
  PS /home/Ps_user> $PSHOME                     
  /opt/microsoft/powershell/7
```

The CurrentUserCurrentHost ```$PROFILE.CurrentUserCurrentHost``` is known as your powershell profile.

To view all the **current properties** of ```$profile```, use the following command:
```bash
  PS /home/Ps_user> $PROFILE | Get-Member -Type NoteProperty | ft -AutoSize

     TypeName: System.String

  Name                   MemberType   Definition
  ----                   ----------   ----------
  AllUsersAllHosts       NoteProperty string AllUsersAllHosts=/opt/microsoft/powershell/7/profile.ps1
  AllUsersCurrentHost    NoteProperty string AllUsersCurrentHost=/opt/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
  CurrentUserAllHosts    NoteProperty string CurrentUserAllHosts=/home/Ps_user/.config/powershell/profile.ps1
  CurrentUserCurrentHost NoteProperty string CurrentUserCurrentHost=/home/Ps_user/.config/powershell/Microsoft.PowerShell_profile.ps1
```
As viewed The ```$PROFILE``` Variable have load of Properties, however the ```$profile``` variable value is **your CurrentUserCurrentHost.**
```bash
PS /home/Ps_user> $PROFILE      
/home/Ps_user/.config/powershell/Microsoft.PowerShell_profile.ps1
PS /home/Ps_user> $PROFILE.CurrentUserCurrentHost
/home/Ps_user/.config/powershell/Microsoft.PowerShell_profile.ps1
```

To view all **the current Members**, use the following command:

```bash
  PS /home/Ps_user> $PROFILE | gm | ft -AutoSize                           

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

*To understand the ```get-memeber```, follow this article, **Command discovery** section: [Command discovery](https://github.com/Ps_user-Eleraki/PowerShell_Articles/tree/main/PsFoldersize#psfoldersize-module-1)*


## Edit Profile


To ensure the **profile path exist** entering this:

```bash
  PS /home/Ps_user> Test-Path -path $PROFILE
  False
  PS /home/Ps_user> Test-Path -path $PROFILE.AllUsersAllHosts
  False
```
The value is False duo to we **didn't create the profiles yet**, to creat **PowerShell Profile** without overwriting an existing profile, use the following:

```bash
  PS /home/Ps_user> if(!(Test-Path -Path $PROFILE)) {New-Item -Type File -path $PROFILE -Force}

      Directory: /home/Ps_user/.config/powershell

  UnixMode   User             Group                 LastWriteTime           Size Name
  --------   ----             -----                 -------------           ---- ----
  -rw-rw-r-- Ps_user          Ps_user              5/6/2023 10:53              0 Microsoft.PowerShell_profile.ps1
```

Let's **edit your profile** using the following command:

```bash
  nano $PROFILE
```

If you're using Windows use the following command:

```bash
  notepad $PROFILE
```

Let's type ```Receive-output``` **Function**:

```bash
  function receive-output
  {
  process {
                  write-host "Value = " -nonewline
                  write-host $_ -ForegroundColor Red -backgroundcolor yellow
          }
  }
```
*This function will print-out the value you're passing to.*

Save, Exit, and restart the PowerShell terminal; Let's try-out The Function by entering the following:

```bash
  PS /home/Ps_user> Write-Output "Ps_user" | Receive-output
  Value = Ps_user
```


## References:

- [About Profiles](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.3)

- [Mastering Windows Server 2016](https://www.amazon.com/Mastering-Windows-Server-Brian-Svidergol/dp/1119404975/ref=sr_1_1?crid=1410D3AZEKH9O&keywords=mastering+windows+server+2016&qid=1683395968&sprefix=Mastering+Windows+Server%2Caps%2C258&sr=8-1)