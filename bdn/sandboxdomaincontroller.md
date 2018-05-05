---
layout: kab
title: Deploy Sandbox Active Directory Domain Controller
group: bdn
---

### Sandbox Active Directory Domain Controller

I occasionally need one of these for evaluation or protopyping.  
NOTE that I am creating the root Active Directory domain beta.fubar.local.

#### The Basics

- Spin up virtual machine and do clean install of Windows Server 2008 R2 (or whatever Windows Server version is appropriate for your project).
- Apply patches to get it current (often an epic test of your patience and determination).
- Do yourself a favor: snapshot your pristine server install so you can return to this happy place
- run `dcpromo` and follow wizard to conclusion
- restart server

#### If you need a self-signed cert to bind to LDAPS

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

#### Add some fake users

I used the [RANDOM USER GENERATOR](https://randomuser.me/) API with the call below to get a comma delimited list of 20 users. 
```
https://randomuser.me/api/?results=20&nat=us&inc=name,email,&format=csv&noinfo
```
I saved the above fake user output file to `C:\admin\data\users.txt` on the domain controller.

On the domain controller I launched PowerShell and ran the command `set-executionpolicy remotesigned` to enable me to run locally written scripts.

The I deployed the following script on the domain controller and ran it as administrator:
```
import-module activedirectory

function Get-Password()
{
  $strUcase = Get-Random -Count 2 -InputObject (65..90) | % {[char]$_}
  $strLcase = Get-Random -Count 2 -InputObject (97..122) | % {[char]$_}
  $strSymbol = Get-Random -Count 1 -InputObject "!","^","-","_","."
  $strNumber = Get-Random -Count 1 -InputObject (50..57) | % {[char]$_}
  $strLcase2 = Get-Random -Count 2 -InputObject (97..122) | % {[char]$_}
  $strNumber2 = Get-Random -Count 2 -InputObject (50..57) | % {[char]$_}
  $strUcase2 = Get-Random -Count 1 -InputObject (65..90) | % {[char]$_}
  $strSymbol2 = Get-Random -Count 1 -InputObject  "!","^","-","_","."
  $strCombined = ([string]($strUcase + $strLcase + $strSymbol + $strNumber + $strLcase2 + $strUcase2 + $strSymbol2 + $strNumber2)).replace(" ","")
  return $strCombined
}

$strADOrganizationalUnit = "OU=Employee,OU=Users,OU=_fubar,DC=beta,DC=fubar,DC=local"

get-content "C:\admin\data\users.txt"|foreach{
  $arrLine = $_.split(",")
  $strSamaccountname = $arrLine[1].substring(0,1) + $arrLine[2]
  if($strSamaccountname.length -gt 20){$strSamaccountname = $strSamaccountname.substring(0,20)}
  $strGivenname = [string]($arrLine[1])
  $strSurname = [string]($arrLine[2])
  $strEmail = [string]($arrLine[3])
  # Obtain password and convert to securestring
  $encPassword = $(get-password) | ConvertTo-SecureString -AsPlainText -Force
  # Attempt actual object creation
  new-aduser -name $strSamaccountName -givenname $strGivenname -surname $strSurname -samaccountname $strSamaccountName -accountpassword $encPassword -path $strADOrganizationalUnit -otherattributes @{mail="$strEmail"} -enabled:$true -passthru -confirm:$false -verbose
  write-host "sleep 1 ========================"
  start-sleep -seconds 1
  clear-variable arrLine,strSamaccountname,strGivenname,strSurname,strEmail,encPassword

}
```


<br/>
<br/>
