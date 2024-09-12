---
created: <% tp.file.creation_date() %>
tags:
  - CS131
  - SJSU
---
## Why make a shell script
- to store commands in file for use with logic and control structure (ie for loops)
	- Scripts can be used to
		- run front end scripts
		- storing several commands with a single command
		- to record the steps thtat it took to accomplish a task

## Steps to write and run a shell script
-  make dir in home dir called `<lastnameF>_4.shell`
- cd into
- make a new file class_practice.sh
- in the file add the following:
```bash
 #!/bin/bash
 
 NAME=$1
 
 echo "Hello, $NAME"
 ```
 - :wq to write and quit
 - run the command `sh class_practice.sh<Your name>`

## some jargon
**Shell** - a program that allows a user to interact with operating system
**Bash** - a unix shell and scripting language
**Shell Script** a scripting language that is run by a shell
**Shebang** - the syntax #! is called shebang
- Script language must begin with this syntax so machine knows which language you are using for your script
- #! is followed by path ot interpreter for the scripting language
- For bash (i.e. Unix OS) this is #!/bin/bash

![[Pasted image 20240909091808.png]]
![[Pasted image 20240909091824.png]]

## Variables 
- SYmbolix names that represent values stored in memory
- three different types of varaibles
- Global Variables: environment and configuration variables capitalized such as `Home, Path, SHell, USERNAME, and PWD`
- Local Variables: vars created within a shell script. Any varaible created in this manner remains in existence only within that shell
- Special variables: reserved for OS, shell programming, etc. such as positional parameters $0, $1
![[Pasted image 20240909092112.png]]
![[Pasted image 20240909092120.png]]
![[Pasted image 20240909092129.png]]
![[Pasted image 20240909092221.png]]
![[Pasted image 20240909093635.png]]
![[Pasted image 20240909093644.png]]
![[Pasted image 20240909093659.png]]
- A and C
![[Pasted image 20240909093716.png]]
- E 
![[Pasted image 20240909093733.png]]
![[Pasted image 20240909093744.png]]
- **IMPORTANT ^** 
![[Pasted image 20240909094307.png]]
## EXIT CODES IN C
- in C, when program completes, it calls the funciton exit with an argument of 0
- The function `exit` terminates  a program
- By convention, an exit code of 0 means OK, and an exit code between 1 and 225 mean that an error occured

![[Pasted image 20240909094428.png]]
![[Pasted image 20240909094439.png]]



