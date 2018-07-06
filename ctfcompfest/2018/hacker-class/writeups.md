# CTF Compfest UI Hacker Class - 2018

Topics:
- [Web](#web)
- [Miscellaneous](#miscellaneous)

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


