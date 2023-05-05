# PowerShell Profiles


## Problems solved:

  - **Senario 01:** You are usnig PowerShell to create bunch of AD users from excel sheet, Using script like the below:

  ```bash
    # This script for clearification only, and not tested! 
    ​import-csv -path c:\temp\users.csv | foreach {

    $givenName = $_.name.split()[0] 
    $surname = $_.name.split()[1]
    new-aduser -name $_.name -enabled $true –givenName $givenName –surname $surname -accountpassword (convertto-securestring $_.password -asplaintext -force) -changepasswordatlogon $true -samaccountname $_.samaccountname –userprincipalname ($_.samaccountname+”@ad.contoso.com”) -city $_.city -department $_.department
    }
  ``` 
  
  each time you'll go and open-up your script and edit the ```import-csv``` path to refer to the new excel sheet you want to woke on. These steps are a little overwhelming. Instead you can define this script as a function in powershell profile and parameterize the ```import-csv``` path, Now each time to create bunch of users just open the PowerSell terminal and type the name of function and send the new path of your excel sheet.


  - **Senario 02:** You have multiple scripts in your environment, and you have some variables, and functinos that you're using continuously in each script, in short period you'll figure out that your script become complix; To make the script simple in as posible you can define all those variables and function in PowerShell profile and just recall it in your script.



You can create a PowerShell profile to customize your environment, You can add commands, aliases, functions, variables, modules, PowerShell drives and more. You can also add other session-specific elements to your profile so they're available in every session without having to import or re-create them. A PowerShell profile is a script that runs when PowerShell starts. You can have multiple profiles per user ####################

the host for powershell host not the machine if you want to navigating on machins with the same profile use onedrive.