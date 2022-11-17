# js-fingerprint-redirect

While analyzing an attack in the wild I saw victims being redirected to a website hosting <a href="index.html">index.html</a> (slightly beautified). 
The JavaScript code in the file does some very interesting fingerprinting before redirecting the user (perhaps based on fingerprint?). 

The code has 88 functions, A1 to A92 (with some gaps), each probing/testing different properties. The goal of this project is to analyze and explain what each function does and why. And of course, understand how these are used in the rest of the script. 

Please feel free to add information about the script or the individual functions. Perhaps this is a known library already? Help with deobfuscation is also appreciated! 


# General functions
<code>go()</code>  Returns the OS based on <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent">Navigator.userAgent</a>. 
Very similar to this code in FingerprintJS https://github.com/fingerprintjs/fingerprintjs/blob/bf7039da92655f981b2b958bb51a031e15601dbe/fingerprint2.js#L1110-L1129

<code>gb()</code> Returns the browser based on <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent">Navigator.userAgent</a>.  

# Fingerprinting functions
Each function $A_i$ return a string containing " $a_i$ : $v$ ", where $v$ is usually $0$, $1$, $e$ for exception. But in general $v$ can have any value. For example, A70 might return "a70:24", where 24 is the <code>window.screen.colorDepth</code>.


For each function I think it would be good to add:
- What does the code do?
- Why does it do it?
- Links and references.

## A1
Returns 1 if the two first characters in <code>navigator.language</code> is 
the same as the two first characters in <code>navigator.languages[0]</code>.

This should always be true as per the standard: 
https://developer.mozilla.org/en-US/docs/Web/API/Navigator/languages


Maybe stolen from https://github.com/fingerprintjs/fingerprintjs 

It is very similar to <code>getHasLiedLanguages</code> that checks if the client is lying about its languages.
This is in version 2.1.0, can't find it in the latest version.

https://github.com/fingerprintjs/fingerprintjs/blob/bf7039da92655f981b2b958bb51a031e15601dbe/fingerprint2.js#L1091-L1105



## A2

Does a few comparisons of screen width and height to available width and height, using
<code>window.screen.width</code>, <code>window.screen.availWidth</code>, etc. 

Once again, similar to fingerprint JS, in particular <code>getHasLiedResolution</code>  https://github.com/fingerprintjs/fingerprintjs/blob/bf7039da92655f981b2b958bb51a031e15601dbe/fingerprint2.js#L1106-L1108

However, in this code they do more checks, including this with the magic number 0x14 = 20 in decimal. 
<code>
window[ 'screen' ][ 'width' ] === window[ 'screen' ][ 'availHeight' ] + 0x14
</code>


## A3
Tries to detect if the client is lying about its OS by comparing <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/oscpu">Navigator.oscpu</a> and the
<a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent">Navigator.userAgent</a>.

Again, copying FingerprintJS: <a href="https://github.com/fingerprintjs/fingerprintjs/blob/bf7039da92655f981b2b958bb51a031e15601dbe/fingerprint2.js#L1139-L1152">fingerprint2.js:1139-1152</a>.


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

Simple color depth check. 

https://developer.mozilla.org/en-US/docs/Web/API/Screen/colorDepth




## A71
## A72
## A73
## A74
## A75
Checks if the function <code>navigator.sendBeacon</code> is available. 

https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon



## A76
Checks if the function <code>navigator.geolocation</code> is available. 

https://developer.mozilla.org/en-US/docs/Web/API/Navigator/geolocation


## A77
Returns 'true' if Puppeteer is used.

Throws an error with <code>new Error( 'Test Error' );</code> then inspects the stack trace looking for
<code>puppeteer_evaluation_script</code>


https://github.com/digitalhurricane-io/puppeteer-detection-100-percent/blob/master/public/main.js

https://www.blackhatworld.com/seo/how-to-detect-puppeteer-with-100-accuracy.1235754/


## A78
Also checks if Puppeteer is used.


First triggers an exception using <code>document.createElement(0);</code>
then looks for a line in the stack trace matching the regex 
<code>/Ob[cej]{3}t\.a[lp]{3}y[\(< ]{3}an[oynm]{5}us>/</code>. 
For example matching <code>Object.apply (<anonymous>:80:31)</code>.

Related: 

https://github.com/berstend/puppeteer-extra/issues/318


Similar code was also found in the wild in this report:  https://www.joesandbox.com/analysis/598617/0/lighthtml




## A79
## A83
Work in progress / TODO 

Seems to compare speed for array push/pop vs adding/removing to localStorage using setItem and removeItem.

When I tried on both Chrome and Firefox, the number of operations for localStorage was orders of magnitude lower than for the array. 
Maybe Puppeteer or similar implement localStorage as an array? 



## A84
## A85
## A86
## A87
## A88
## A89
## A90
## A91
## A92
