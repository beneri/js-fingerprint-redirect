# js-fingerprint-redirect

While analyzing an attack in the wild I saw victims being redirected to a website hosting <a href="index.html">index.html</a> (slightly beautified). 
The JavaScript code in the file does some very interesting fingerprinting before redirecting the user (perhaps based on fingerprint?). 

The code has 88 functions, A1 to A92 (with some gaps), each probing/testing different properties. The goal of this project is to analyze and explain what each function does and why. And of course, understand how these are used in the rest of the script. 

Please feel free to add information about the script or the individual functions. Perhaps this is a known library already? Help with deobfuscation is also appreciated! 


# Fingerprinting functions
Each function $A_i$ return a string containg " $a_i$ : $v$ ", where $v$ is usally $0$, $1$, $n$, or $e$ for exception. For example, A70 might return "a70:24", where 24 is the <code>window.screen.colorDepth</code>.


For each function I think it would be good to add:
- What does the code do?
- Why does it do it?
- Links and references.

## A1
## A2
## A3
## A4
## A5
## A6
## A7
## A8
## A9
## A10
## A11
## A12
## A13
## A14
## A15
## A16
## A17
## A18
## A19
## A20
## A21
## A22
## A23
## A24
## A25
## A26
## A27
## A28
## A29
## A30
## A31
## A32
## A33
## A34
## A35
## A36
## A37
## A38
## A39
## A40
## A42
## A43
## A44
## A45
## A46
## A47
## A48
## A49
## A50
## A51
## A52
## A53
## A54
## A55
## A56
## A57
## A58
## A59

Returns 1 if Kaspersky is detected. 
Looks for an element with id "frmin" and then checks for related strings, such as "kaspersky"


Code is very similar to: <a href="https://vah13.github.io/AVDetection/">https://vah13.github.io/AVDetection/</a>.

## A60
## A61
## A62
## A63
## A64
## A65
## A66
## A67
## A68
## A69
## A70
## A71
## A72
## A73
## A74
## A75
## A76
## A77
## A78
## A79
## A83
## A84
## A85
## A86
## A87
## A88
## A89
## A90
## A91
## A92
