#Rshell
This project is a shell that interprets and executes lines of command, including the commands, their arguments, and connectors. 
It simulates the functionality of the bash shell. This project is made for an assignment for the CS100 course, a course on open
source software construction, at University of California, Riverside. 

Included is also an implementation of the `ls` program, which is supposed to be as close to the GNU `ls` program as possible. My ls program supports the `-l`, `-a`, and `-R` flags.
##Dependencies
rshell requires the Boost Libraries for C++ to be installed. 

The UCR lab machines, with cs100 settings, already have the Boost Libraries installed.

To install the libraries on Linux Mint, run `sudo apt-get install libboost-all-dev`

Otherwise, download Boost from [www.boost.org/users/download/](www.boost.org/users/download/)
##Install/Run 
To install, type the following into the terminal:
```
$ git clone https://github.com/pockymons/rshell.git
$ cd rshell
$ git checkout hw0
$ make
```

To run, type the following into the terminal, while you are in the rshell directory:
```
$ bin/rshell
```
##Edge Cases
###rshell
* I chose to make comments only work if there is a space before the `#` symbol, just like bash does it.
* Connectors are ordered from left to right. The command before a connector is checked for each connector. There is no order of precedence.
* Whitespace followed by a connector will have the same effect as a `;` connector. For example, the following code will have the same result as the `ls` command.
```
        && ls
```

##Limitations/Bugs
### rshell
* Prompt only works for up to 64 characters.
* If there is whitespace only after a connector, it will just act as if it is then end, instead of outputting an error message.
* Pressing the up arrow key does not go to the previous command
* Press tab does not auto-complete a command/directory
* The `||` and `&&` connectors only work in even groupings. Otherwise, they are interpreted as commands or part of a command.
* Comments only work if there is a command preceding them. If a line has nothing but a comment, there will be an error.
* "Built-in" bash commands are not executed (such as cd).
* If a connector is the first text in a line, there will be unintended or unexpected behavior. For the `&&` and `;` connectors, the following command will be run twice. However, the `||` connector will behave as expected and just run the command once. However, if there is some whitespace then the connector will behave as it described in the Edge Cases section. This means that the following line will behave as though there is no whitespace and no `;` connector in the beginning and just run the `ls` command.
```
       ; ls
```
### ls
* The GNU `ls` program will output the year in the `-l` flag, if the last modified date is older than 6 months. My program does not.
* My program does not list the symbolic links.
* Files are not printed in the same line.
* The `-R` flag has spacing inconsistencies, including an extra space at the end of the output as well as if a directory has no files.
