# CTF Compfest UI Hacker Class - 2018

Topics:
- [Web](#web)
- [Cryptography](#cryptography)

## Web
### > Find The Flag in Homepage - 50pts
Find the flag in homepage ctf.compfest.web.id

**Solution:**  
Inspect element on browser and copy the flag.  
<br>

### > You Gender Is Male - 274pts
You solve this problem as a Man. Man is always wrong, woman is always right. Guess the number at: http://103.200.4.156:8350/

**Solution:**  
The vulnerability of `index.php` is `extract($_POST)` as shown in this code.
```
<?php
  include 'flag.php';
  if (isset($_POST['guess'])) {
    extract($_POST);
    if ($guess == $number) {
      die($flag);
    }
  }
?>
``` 
With `extract` function and `$_POST` as it's parameter, you can modify $guess and $number variable by sending POST request to http://103.200.4.156:8350/ with `guess` and `number` as it's parameter. For example, if you use postman, you can fill the POST body like this.  

| key | value |
| ----- | -----: |
| guess | 1 |
| number | 1 |

After that, you will receive the flag in the response body.  
<br>

## Cryptography
### > Xorry - 70pts
Run the attached script with:  
`python3 xorry.py`  
Good luck! :)

```
#!/usr/bin/python3
import base64

secret_data = ("AAAAUgNLEkdTBh5FNzwvNhxJBH8EDjEHTwYdWSsDAx5/EDAWFQYRLQhGGEUsDj"
               "ICGwcNMQJOClIOERodTxowVBwEGDNZFhoqFwkLBjpFAUUSBBAK")
secret_password = ("\x45\x5a\x56\x46\x54\x15\x40\x14\x42\x5d\x5e\x51\x45\x5a"
                   "\x5a\x5a\x56\x12\x5a\x14\x46\x53\x5d\x40\x11\x46\x5c\x14"
                   "\x45\x57\x5f\x58\x11\x4b\x5c\x41")

def y(s1, s2):
    len1 = len(s1)
    len2 = len(s2)
    res = ""
    for i in range(len1):
        chr1 = ord(s1[i]) ^ ord(s2[i % len2])
        res += chr(chr1)
    return res

inp = input("Input your password to get the flag :")

wwhatisthisvariable = y(inp, '1234')
if wwhatisthisvariable == secret_password:
    d1, d2 = base64.b64decode(secret_data).decode('utf-8'), inp
    print("Horray, you've cracked the password!!")
    print(y(d1, d2))
```

**Solution:**  
To get the flag, `wwhatisthisvariable` variable must have the same value as `secret_password` variable. We can see that the operation in function y only using XOR to encrypt the string. The operation is XOR between the plain text and the key. The key to encrypt the plain text is `1234`. So, to get the the plain text, do XOR operation between secret_password and `1234`. After you get the plain text, just do the operation inside the conditional and you will get the flag.  
<br>

### > Caesar - 50 pts
ULXP{a_lzafc_lzak_hjgtwde_ak_lgg_wskq_xgj_qgm_kg_a_oadd_ljq_lg_escw_kgewlzafy_zsjvwj_fwpl_laew}

**Solution:**  
Use Caesar Cipher to decript the ciphertext flag.  
<br>

