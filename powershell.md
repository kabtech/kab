---
layout: page
---
[RETURN TO axis >>](http://axis.bestul.us)

## PowerShell

#### Setup an array-input construct which awaits pasted list to populate the array
```
#Hit ctrl-C after you paste, at which point your populated array is ready for use.
$arrList = @();while (!$strStop){$arrList += read-host "Next entry:"}
#Or...use a construct like this if you want to be able to signal to a running script that you are done pasting entries:
while ($arrList -notcontains "swordfish"){$arrList += read-host "Paste list or type 'swordfish' to indicate paste is done"}
```
#### Check if file is locked - the following construct can be used so that $intLocked is an indicator whether you may access a file to write:
```
try { [IO.File]::OpenWrite($FilePath).close();$intLocked = 0}
catch{$intLocked = 1}
```


