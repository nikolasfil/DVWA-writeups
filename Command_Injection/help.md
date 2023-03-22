# About

*(from the help page of the challenge)*

The purpose of the command injection attack is to inject and execute commands specified by the attacker in the vulnerable application. In situation like this, the application, which executes unwanted system commands, is like a pseudo system shell, and the attacker may use it as any authorized system user. However, commands are executed with the same privileges and environment as the web service has.

**Command injection** attacks are possible in most cases because of lack of correct input data validation, which can be manipulated by the attacker (forms, cookies, HTTP headers etc.).

The syntax and commands may differ between the Operating Systems (OS), such as Linux and Windows, depending on their desired actions.

This attack may also be called "Remote Command Execution (RCE)".



## Objective
Remotely, find out the user of the web service on the OS, as well as the machines hostname via RCE.



### Low Level
This allows for direct input into one of many PHP functions that will execute commands on the OS. It is possible to escape out of the designed command and executed unintentional actions.

This can be done by adding on to the request, "once the command has executed successfully, run this command".



### Medium Level
The developer has read up on some of the issues with command injection, and placed in various pattern patching to filter the input. However, this isn't enough.

Various other system syntaxes can be used to break out of the desired command.



### High Level
In the high level, the developer goes back to the drawing board and puts in even more pattern to match. But even this isn't enough.

The developer has either made a slight typo with the filters and believes a certain PHP command will save them from this mistake.




### Impossible Level
In the impossible level, the challenge has been re-written, only to allow a very stricted input. If this doesn't match and doesn't produce a certain result, it will not be allowed to execute. Rather than "black listing" filtering (allowing any input and removing unwanted), this uses "white listing" (only allow certain values).

