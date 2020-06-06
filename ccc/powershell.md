---
layout: kab
title: PowerShell
group: ccc
---
### PowerShell

#### Setup an array-input construct which awaits pasted list to populate the array
```
#Hit ctrl-C after you paste, at which point your populated array is ready for use.
$arrList = @();while (!$strStop){$arrList += read-host "Next entry:"}
#Or...use a construct like this if you want to be able to signal to a running script that you are done pasting entries:
$arrList = @();while ($arrList -notcontains "swordfish"){$arrList += read-host "Paste list or type 'swordfish' to indicate paste is done"}
```

#### Convert BASE64 encoded string of a file back to its original binary file type
```
$strEncodedFilePath = "C:\yourpath\base64encodedpdf.pem"
$strDecodedFilePath = "C:\yourpath\restoredusablepdf.pdf"
[System.Convert]::FromBase64String((Get-Content $strEncodedFilePath)) | Set-Content $strDecodedFilePath -Encoding Byte
```

#### Check if file is locked - the following construct can be used so that $intLocked is an indicator whether you may access a file to write:
```
try { [IO.File]::OpenWrite($FilePath).close();$intLocked = 0}
catch{$intLocked = 1}
```

#### Use Invoke-Command to run command on the remote server instead local host | sends command across the wire for the remote server to execute. NOTE use of 'using:' scope notation to embed a local varible into the script block:
```
$objMailbox = invoke-command -session (get-pssession) -scriptblock {get-mailbox $using:strUser -ea silentlycontinue| select-object -property PrimarySMTPAddress}
```

#### Universal sortable date format:
```
$dtmNow = (Get-Date).ToUniversalTime()
$strDate = [string](Get-Date -date $dtmNow -format "yyyy-MM-ddTHH:mm:ss.fffZ")
```

#### Windows token size analysis best script:
```
https://gallery.technet.microsoft.com/scriptcenter/Check-for-MaxTokenSize-520e51e5?ranMID=24542&ranEAID=je6NUbpObpQ&ranSiteID=je6NUbpObpQ-M8djojEYyzA6NWZdgiWVaA&tduid=(e9c9e889f21b093f683dc9c0e1d3938f)(256380)(2459594)(je6NUbpObpQ-M8djojEYyzA6NWZdgiWVaA)()
```

#### Change password on user object using the activedirectory module:
```
$strPass = "CYgX-4prM_75"
$encPass = $strPass | ConvertTo-SecureString -AsPlainText -Force
Set-ADAccountPassword -id joeuser -NewPassword $encPass -reset
```

#### Measure time to CURL a website with and without proxy for comparison of results:
```
(measure-command{Invoke-WebRequest -Uri http://www.noaa.gov -Method Get}).milliseconds
(measure-command{Invoke-WebRequest -Uri http://www.noaa.gov -Method Get -proxy http://proxyserver.fubar.com:8080}).milliseconds
```

#### Retrieve the members of local groups:
```
Add-Type -AssemblyName System.DirectoryServices.AccountManagement
$ctype = [System.DirectoryServices.AccountManagement.ContextType]::Machine
$servers = Get-ADComputer -resultsetsize $null -searchbase "OU=DHPServers,OU=_DHP,DC=dhp,DC=ad,DC=deanhealth,DC=com" -searchscope subtree -Filter `
{(samaccountname -like "DHP*MV*P*")}
$servers | foreach {write-host "============================";$serverName = $_.name;$context = New-Object -TypeName System.DirectoryServices.AccountManagement.PrincipalContext -ArgumentList $ctype, $serverName;$idtype = [System.DirectoryServices.AccountManagement.IdentityType]::SamAccountName;$group = [System.DirectoryServices.AccountManagement.GroupPrincipal]::FindByIdentity($context, $idtype, 'Administrators');$group.Members | select @{N='Domain'; E={$_.Context.Name}}, samaccountName}
```

#### PowerShell grep equivalents:
```
#grep equivalent
select-string "citd" -path uwcxdcasa_030212a.txt | out-string -width 4096 | out-file c:\downloads\citd.txt
#the 'out' parameters create an output file that is not wrapped like the screen output
select-string "Advisors\+Recruiters\+List\+Oct\+2011" -path ex1*.* | out -string -width 500 | out-file Y:\_grep.txt
#meet 2 conditions (and), not case sensitive
select-string -pattern "^(?=.*JPMorgan)(?=.*ECQA)"
#recursive
get-childitem c:\ -include *.txt -rec | select-string -pattern "\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,6}"
get-childitem "\\dhp\SystemDFS\Users" -include ServiceRequest*.txt -rec | select-string -pattern "ftp" -context 3,2
#show lines before and after:
Select-String C:\Scripts\Test.lxt -pattern "failure" -context 3,1
```

#### List permissions on an AD object:
```
get-adpermission -id "System Management"  | Where { $_.User -like "*PAPP00*" } | fl
```

#### List all sites on a particular IIS server:
```
add-pssnapin WebAdministration
get-childitem 'IIS:\sites\*' | out-string -width 140 | out-file c:\downloads\sites.txt
```

#### ICACLS equivalent:
```
$kab = get-acl -path \\dhp\systemdfs
$kab.access | where {$_.identityreference -like "DHP\*" -or $_.identityreference -like "BUILTIN\*"} | fl
```

#### Get the ascii value of an unknown character
```
[int][char]'�'
```

#### Replace a special character using the regex notation
```
$strParentSite = $strParentSite -replace "$([char]65533)", "-"
```

#### Retrieve the share level permissions of a share on a selected computer
```
$share = 'data$'
$remotecomputer = "dhpsec"
$query = "Associators of {win32_LogicalShareSecuritySetting='$share'} Where resultclass = win32_sid"
Get-WmiObject -query $query -cn $remotecomputer
```

#### Perform comparison of 2 text files
```
$comparisonresult = Compare-Object -ReferenceObject (Get-Content .\diskcapacity.csv) -DifferenceObject (Get-Content .\diskcapacity2.csv)
$comparisonresult | fl
#append the ' -IncludeEqual' parameter onto the end of the first command to have the comparison of every line whether or not a difference is found
```

#### DNS lookup - forward and reverse
```
[System.Net.Dns]::GetHostAddresses("www.google.com")
[System.Net.Dns]::GetHostByAddress($strTargetIP)
```

#### Encrypted password file methodology
```
#One time process to encrypt and store password -- run at command line
$strInputPassword = "swordfish"
$encPswd = convertto-securestring $strInputPassword -asplaintext -force
$encPswd | ConvertFrom-SecureString | Set-Content C:\admin\scripts\dev\_testcredstore.txt
clear-variable encPswd #cleanup
clear-variable strInputPassword

#use in script to retrieve encrypted password from file and convert back to plaintext
$encPswd = get-Content C:\admin\scripts\dev\_testcredstore.txt | ConvertTo-SecureString
$marshal = [System.Runtime.InteropServices.Marshal]
$objPointer = $marshal::SecureStringToBSTR( $encPswd )
$strRetrievedPassword = $marshal::PtrToStringBSTR( $objPointer )
$marshal::ZeroFreeBSTR( $objPointer )
$strRetrievedPassword
```

#### Change a registry entry value
```
Set-ItemProperty -Path "HKLM:\SOFTWARE\Wow6432Node\Robo-FTP 3.8\FTPServers\TurboSite" -Name ServerName -Value "server.c.com"
```

#### Create new domain local security group and add members
```
New-ADGroup -Name zzz -SamAccountName zzz -DisplayName zzz -Description "www" -Path "OU=aaa,DC=bbb,DC=ccc,DC=com" -GroupScope DomainLocal -GroupCategory Security
Add-ADGroupMember -Identity zzz -Members yyy(comma separated list of samaccountnames works)
```

#### Use ADSI to get membership of a group (handy in cases where ActiveDirectory module is not supported
```
$objGroup = [ADSI]"LDAP://CN=Schema Admins,CN=Builtin,DC=ad,DC=fubar,DC=com";$objGroup.invoke("Members")|foreach{$_.GetType().InvokeMember("DistinguishedName", 'GetProperty', $null, $_, $null)} | sort
```

#### Get DNS zone resource records
```
import-module dnsserver
Get-DnsServerResourceRecord -ZoneName "contoso.com" -ComputerName dc1.contoso.com -rrtype "A" | where{!$_.timestamp -and $_.hostname -notlike "dhpx*"}
HostName                  RecordType Timestamp            TimeToLive      RecordData
```

#### Cross forest user object relationships for lync and exchange
```
#msExchRecipientTypeDetails=128 #mail-enabled user
#msExchRecipientTypeDetails=1 #user mailbox
get-aduser -id gblanston -properties emailaddress,targetAddress,msExchRecipientTypeDetails,msRTCSIP-PrimaryUserAddress,msRTCSIP-UserEnabled
#DHP object (mailuser pointing to DS object):
#msExchRecipientTypeDetails : 128
#targetAddress              : SMTP:Gern_Blanston@fubar.com (secondary SMTP address on DS object)
#DS object (mailbox-enabled user):
#msExchRecipientTypeDetails : 1
#msRTCSIP-PrimaryUserAddress : sip:Gern.Blanston@fubar.com
#msRTCSIP-UserEnabled        : True
```

#### Accessing registry values with get-childitem and get-itemproperty
```
$strPath = "HKLM:\SOFTWARE\Wow6432Node\Robo-FTP 3.8\FTPServers"
$objKeyCollection = get-childitem -path $strPath | foreach{($_.name).replace("HKEY_LOCAL_MACHINE","HKLM:")}
$objValueCollection = foreach($objKey in $objKeyCollection){Get-Itemproperty -path $objKey | foreach{$strOutput = $_.SiteName + "|" + $_.ServerName;$strOutput}}
```

#### Use certutil on CA to enumerate certs within x days of expiration
```
[int]$InNumberOfDays=90
$today=Get-Date
$endperiod=$today.AddDays($InNumberOfDays)
$objExport=certutil -view -restrict "NotAfter>=$today,NotAfter<=$endperiod" -out "RequestID,RequesterName,RequestType,NotAfter,CommonName,EnrollmentFlags"
$arrCerts=$objExport -match "Row \d*:"
```

#### Identify all certs that do not autoenroll
```
$arrCerts=certutil -view -restrict "enrollmentflags=0" -out "RequestID,RequesterName,RequestType,NotAfter,CommonName,EnrollmentFlags"
```

#### Retrieve all PKI enrollment services at a given OU, including their host server name. Note that results may not be returned if you do not specify a searchbase.
```
get-adobject -ResultSetSize $null -filter{ObjectClass -eq "pKIEnrollmentService"} -searchbase "CN=Enrollment Services,CN=Public Key Services,CN=Services,CN=Configuration,DC=ad,DC=fubar,DC=com" -properties dnshostname
```

#### CURL equivalent that is not dependent on PowerShell version (NOTE that there is also a .DownloadFile method which could be handy):
```
$webclient = new-object system.net.webclient
$webclient.DownloadString('http://google.com')
```

#### CURL with purposeful modification to available cryptography protocol:
```
#ServicePointManager.SecurityProtocol = SecurityProtocolType.Ssl3 | SecurityProtocolType.Tls | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12;
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12;
$web = New-Object Net.WebClient
$web.DownloadString("https://fubar.com:9744/productdesign/fubar/")
==========================================
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Ssl3;
$web = New-Object Net.WebClient
$web.DownloadString("https://fubar.com/fubar/")
```

#### Get PowerShell version of current shell:
```
$PSVersionTable.PSVersion
```


<br/>
<br/>
<br/>
