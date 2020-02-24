---
layout: kab
group: rs
title: Java
---

### Java

```
The package is the group of related interfaces and classes.

CASE CONVENTIONS:
package name | lowercase
class name | pascal case (1st letter lower)
variables | camel case; can also contain numbers, $, and _; cannot start with a number; starting with letter is preferred
object name | pascal case

CODE CONVENTIONS:
// indicates a one line comment
/* ... */ encloses a multi line comment
; marks the end of a command/statement in the code
declare a variable with its type | int userAge; | results in memory space allocation
Any variable declared must be assigned a value (initialized), either in the declaration or separate
Unusual operators: 
  += (add 1 to the variable)
  -= (subtract 1 from the variable)
  *= (variable times inverted ratio)
String is a hybrid primitive type, as it has object methods like length()
When defining a method (public static void main(String[]args))
  static means that the method is associated with the class, not a specific instance (object) of that class
  void means that the method has no return value.

VARIABLE TYPES
Integers or whole numbers: byte, short, int, long 
Floating point: float, double
Other: char, boolean
String is a hybrid primitive type, as it has object methods like length()
Array: int[] arrMemberCount = new int[12] | dataType[] arrName= new dataType[array size];


WHEN YOU ARE READY TO VALIDATE YOUR CREATED/MODIFIED CODE:
Save changes |File>Save
Compile code | Source>Compile code
Run | 


SOME NATIVE PACKAGES PRESENT FOR IMPORT WHEN NEEDED:
java.awt = gui components (menus, buttons, etc)
java.io = i/o components
```

Compile and run your .java file:
```
#COMPILE======================
javac -classpath ".;C:\jars\commons-codec-1.7.jar" Base64Example.java
* where classpath must include the jar(s) that contain the class that your code is importing
* where the . in classpath means look in current directory, and the ; is the windows path separator
#RUN==================
java -classpath ".;C:\jars\commons-codec-1.7.jar" Base64Example
* where the . in classpath means look in current directory, and the ; is the windows path separator
```



<br/>
<br/>
