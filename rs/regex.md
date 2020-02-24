---
layout: kab
group: rs
title: Regular Expressions
---

### Regular Expressions Reference

```
————————————————————————————————————————————————————————————————————————————————————————————————————
PATTERN MODIFIERS (switches)
————————————————————————————————————————————————————————————————————————————————————————————————————

i             Case-insensitive
m             Multiline   : allow the grep engine to match at  ^ and $ after and before at \r or \n.
s             Magic Dot   : allows . to match \r and \n
x             Free-spacing: ignore unescaped white space; allow inline comments in grep patterns.

(?imsx)       On
(?-imsx)      Off
(?i-msx)      Mixed

————————————————————————————————————————————————————————————————————————————————————————————————————
Regex Meta-Characters:
————————————————————————————————————————————————————————————————————————————————————————————————————

.             Any character except newline or carriage return
[ ]           Any single character of set
[^ ]          Any single character NOT of set
*             0 or more previous regular expression
*?            0 or more previous regular expression (non-greedy)
+             1 or more previous regular expression
+?            1 or more previous regular expression (non-greedy)
?             0 or 1 previous regular expression
|             Alternation
( )           Grouping regular expressions
^             Beginning of a line or string
$             End of a line or string
{m,n}         At least m but most n previous regular expression
{m,n}?        At least m but most n previous regular expression (non-greedy)
\1-9          Nth previous captured group
\&            Whole match                                     # BBEdit: '&' only - no escape needed
\`            Pre-match                                       # PCRE?  NOT BBEdit
\'            Post-match                                      # PCRE?  NOT BBEdit
\+            Highest group matched                           # PCRE?  NOT BBEdit
\A            Beginning of a string
\b            Backspace(0x08)(inside[]only)                   # PCRE?
\b            Word boundary(outside[]only)
\B            Non-word boundary
\d            Digit, same as[0-9]
\D            Non-digit
\G            Assert position at end of previous match or start of string for first match

————————————————————————————————————————————————————————————————————————————————————————————————————
Case-Change Operators
————————————————————————————————————————————————————————————————————————————————————————————————————
\E            Change case - acts as an end delimiter to terminate runs of \L & \U.
\l            Change case of only the first character to the right lower case. (Note: lowercase 'L')
\L            Change case of all text to the right to lowercase.
\u            Change case of only the first character to the right to uppercase.
\U            Change case of all text to the right to uppercase.

————————————————————————————————————————————————————————————————————————————————————————————————————
White-Space or Non-White-Space
————————————————————————————————————————————————————————————————————————————————————————————————————
\t            Tab
\n            Linefeed
\r            Return
\f            Formfeed
\s            Whitespace character equivalent to [ \t\n\r\f]
\S            Non-whitespace character
————————————————————————————————————————————————————————————————————————————————————————————————————

\W            Non-word character
\w            Word character[0-9A-Za-z_]
\z            End of a string
\Z            End of a string, or before newline at the end
(?#)          Comment
(?:)          Grouping without backreferences
(?=)          Zero-width positive look-ahead assertion
(?!)          Zero-width negative look-ahead assertion
(?>)          Nested anchored sub-regexp stops backtracking
(?imx-imx)    Turns on/off imx options for rest of regexp
(?imx-imx:…)  Turns on/off imx options, localized in group    # '…' indicates added regex pattern

————————————————————————————————————————————————————————————————————————————————————————————————————
PERL-STYLE PATTERN EXTENSIONS : BBEdit Documentation : '…' indicates added regex pattern
————————————————————————————————————————————————————————————————————————————————————————————————————
Extension       Meaning
————————————————————————————————————————————————————————————————————————————————————————————————————
(?:…)           Cluster-only parentheses, no capturing
(?#…)           Comment, discard all text between the parentheses
(?imsx-imsx)    Enable/disable pattern modifiers
(?imsx-imsx:…)  Cluster-only parens with modifiers
(?=…)           Positive lookahead assertion
(?!…)           Negative lookahead assertion
(?<=…)          Positive lookbehind assertion
(?<!…)          Negative lookbehind assertion
(?()…|…)        Match with if-then-else
(?()…)          Match with if-then
(?>…)           Match non-backtracking subpattern (“once-only”)
(?R)            Recursive pattern

————————————————————————————————————————————————————————————————————————————————————————————————————
POSITIONAL ASSERTIONS (duplicatation of above)
————————————————————————————————————————————————————————————————————————————————————————————————————

POSITIVE LOOKAHEAD ASSERTION:   (?='pattern')
NEGATIVE LOOKAHEAD ASSERTION:           (?!'pattern')

POSITIVE LOOKBEHIND ASSERTION:          (?<='pattern') # Lookbehind Assertions are of fixed-length
NEGATIVE LOOKBEHIND ASSERTION:          (?<!'pattern')

————————————————————————————————————————————————————————————————————————————————————————————————————
SPECIAL CHARACTER CLASSES (POSIX standard except where 'Perl Extension' is indicated):
————————————————————————————————————————————————————————————————————————————————————————————————————
CLASS           MEANING
————————————————————————————————————————————————————————————————————————————————————————————————————
[[:alnum:]]     Alpha-numeric characters
[[:alpha:]]     Alphabetic characters
[[:ascii:]]     Character codes 0-127         # Perl Extension
[[:blank:]]     Horizontal whitespace
[[:cntrl:]]     Control characters
[[:digit:]]     Decimal digits (same as \d)
[[:graph:]]     Printing characters, excluding spaces
[[:lower:]]     Lower case letters
[[:print:]]     Printing characters, including spaces
[[:punct:]]     Punctuation characters
[[:space:]]     White space (same as \s)
[[:upper:]]     Upper case letters
[[:word:]]      Word characters (same as \w)  # Perl Extension
[[:xdigit:]]    Hexadecimal digits

Usage example of multiple character classes:

        [[:alpha:][:digit:]]

«Negated» character class example:

        [[:^digit:]]+


** POSIX-style character class names are case-sensitive

** The outermost brackets above indicate a RANGE; the class name itself looks like this: [:alnum:]

————————————————————————————————————————————————————————————————————————————————————————————————————
CONDITIONAL SUBPATTERNS
————————————————————————————————————————————————————————————————————————————————————————————————————

Conditional subpatterns allow you to apply “if-then” or “if-then-else” logic to pattern matching.
The “if” portion can either be an integer between 1 and 99, or an assertion.

The forms of syntax for an ordinary conditional subpattern are:

     if-then: (?(condition)yes-pattern)
if-then-else: (?(condition)yes-pattern|no-pattern)

and for a named conditional subpattern are:

     if-then: (?P<NAME>(condition)yes-pattern)
if-then-else: (?P<NAME>(condition)yes-pattern|no-pattern)

If the condition evaluates as true, the “yes-pattern” portion attempts to match. Otherwise, the
“no-pattern” portion does (if there is a “no-pattern”).
```


<br/>
<br/>
