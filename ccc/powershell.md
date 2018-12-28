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
#### Check if file is locked - the following construct can be used so that $intLocked is an indicator whether you may access a file to write:
```
try { [IO.File]::OpenWrite($FilePath).close();$intLocked = 0}
catch{$intLocked = 1}
```


#### Use Invoke-Command to run command on the remote server instead local host | sends command across the wire for the remote server to execute. NOTE use of 'using:' scope notation to embed a local varible into the script block:
```
$objMailbox = invoke-command -session (get-pssession) -scriptblock {get-mailbox $using:strUser -ea silentlycontinue| select-object -property PrimarySMTPAddress}
```

<br/>
<br/>
<br/>
