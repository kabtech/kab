---
layout: kab
group: ccc
title: VI editor
---

### VI editor

#### Input commands (end with Esc)
```
a Append after cursor
i Insert before cursor
o Open line below
O Open line above
:r file Insert file  after current line
Any of these commands leaves vi in input mode until you
press Esc. Pressing the RETURN key will not take you out
of input mode.
```

#### Change commands (Input mode)
```
cw Change word (Esc)
cc Change line (Esc) - blanks line
c$ Change to end of line
rc Replace character with c
R Replace (Esc) - typeover
s Substitute (Esc) - 1 char with string
S Substitute (Esc) - Rest of line with
text
. Repeat last change
```

#### Changes during insert mode
```
<ctrl>h   Back one character
<ctrl>w   Back one word
<ctrl>u   Back to beginning of insert
```

#### File management commands
```
:w name Write edit buffer to file name
:wq Write to file and quit
:q! Quit without saving changes
ZZ Same as :wq
```



<br/>
<br/>
