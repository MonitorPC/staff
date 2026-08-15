# `exec` command in Bash

**Tested on**: Laptop with Arch + Berry WM setup

## Before we start

Before we moving on to the main part, I want you to tell what I wanted and why.  
All it starts from configuration of Arch(btw). I chose the [Berry WM](https://berrywm.org/) this time.  
My main requests are simplicity and safety.  

In default confs it said just run `startx` command with preconfigured `.xinitrc` file.  
`.xinitrc` file contains one command `exec berry`.
It is really simple but what about safety?  

If close my laptop the X-session will not close and anyone can open laptop and get access to all my files.  
Using a loggin manager is not my way, simple exit from `berry` process will return me in tty shell again less security.
It is where I deep dive into `exec`.

## *In plain English*

As you can know the `exec command` will change the current shell process with command.
So to fullfil my requests I just run `exec startx`.  
And after killing `berry` process I will get getty instead of shell.

But I dont stop on it. `exec >` command... 
