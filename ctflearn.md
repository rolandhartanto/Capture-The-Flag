# CTFLearn Write-ups

Topics:
- [Web Exploitation](#web-exploitation)
- [Miscellaneous](#miscellaneous)
- [Cryptography](#cryptography)
- [Forensics](#forensics)
- [Programming](#programming)
- [Binary Exploitation](#binary-exploitation)

## Web Exploitation
### > Basic Injection - intelagent - 2pts
See if you can leak the whole database. https://web.ctflearn.com/web4/

**Solution:**  
You can input any string to the input field. In this case, you can try SQL Injection to leak the whole database. The flag is in the output.

```
' OR '1' = '1
```
<br>

### > Don't Bump Your Head(er) - intelagent - 4pts
Try to bypass my security measure on this site! https://ctflearn.com/header.php

**Solution:**  
When you visit the site, you can find the clue in the HTML code.
```
<html>
  <head></head>
  <body>
    Sorry, it seems as if your user agent is not correct, in order to access this website. The one you supplied is: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
    
    <!-- Sup3rS3cr3tAg3nt  -->
  </body>
</html>
```

From the clue above, we have to change the user agent to `Sup3rS3cr3tAg3nt` before we send the request to the site.

Using postman, change the user agent to `Sup3rS3cr3tAg3nt` and send GET request to https://ctflearn.com/header.php. You will get this response. 

```
Sorry, it seems as if you did not just come from the site, "awesomesauce.com".
```

You have to change the Referer in the header to awesomesauce.com then you send GET request again to https://ctflearn.com/header.php. The response contains the flag in it.

**Summary:**  
Send request to https://ctflearn.com/header.php with this header:
```
User-Agent: Sup3rS3cr3tAg3nt
Referer: awesomesauce.com
```
<br>

## Miscellaneous


## Cryptography


## Forensics


## Programming
Coming soon

## Binary Exploitation
Coming soon

