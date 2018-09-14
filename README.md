# resgu

Range Expect Script Generator Utility


*Important Notes* 

This utility requires both kornshell (aka ksh) and expect to be installed. I've tested various versions of each without issue, but make no guarantees if the version of ksh or expect that you're using do not work. 

Also, the utility will only work be able to reach your target hosts if you either have passwordless authentication setup for all target hosts or all of the target hosts logins use the same password. I highly recommend the former where possible.

Any user can use the utility (sudo not needed so only give this to users that can be trusted).


Synopsis:

If you don't have an enterprise level automation software available such as Ansible, but have a need to automate a repetetive task to tens, hundreds or even thoughands of servers without creating an expect script everytime you have a new task to do, then give resgu a try. Resgu is a utility which allows for a single string to be sent via sftp or ssh to a range of ip addresses based off a specified host file (sorry ftp is not included due to security issues with the protocol). The utility generates and executes multiple expect scripts on the fly and simultaneously based off the user's interactively inputted criteria. This has been tested via SLES 9 through 11, but should also work for systems that utilize other versions of Linux as well as AIX, Cygwin or OSX (assuming you have both kornshell and expect installed). The utility is written in kornshell and expect so feel free to make your own alterations.


Initial Setup:

There is a very small amount of setup that needs to be done to get the utility to work properly.

1. Placing resgu and the required files.

The resgu executable can only be executed from a users home/user/resgu directory. For instance if I'm logging into the central server as the user "someuser1", then the resgu executable and it's required files must be in the "/home/someuser1/resgu" directory.

2. Setting up the "Users" file

A file called "Users" must be placed in the directory where resgu executable is. Resgu uses this to tell if the remote user is already setup up with passwordless authentication or not. If not you will be prompted to enter a password. First column is the name of the user and the second column should be set to either passwordnotrequired or passwordrequired accordingly.

someuser1 passwordnotrequired
someuser2 passwordrequired
ansibletower passwordrequired
root passwordrequired
...

3. Setting up a single or multiple hosts files. 

One or more hosts files named whatever you'd like must be placed in the directory where the resgu executable is. Resgu uses this to connect to the remote hosts via a range that you select interactively upon execution of the utility. Hosts files must be in a two column format just like a normal hosts file. 

server1 12.34.56.78
server2 12.45.67.89
server3 13.56.78.89
...

Usage:

When you execute the utility you will be greeted with the following information that is relevant to the setup and responses you will be providing before the ultimate execution of the expect scripts.

/------------------------------------------------------\
| Please answer the following questions appropriately. |
\------------------------------------------------------/

1. Users file must be in the following format.
user1  passwordnotrequired 
user2  passwordrequired
user3  passwordrequired
...

2. Hosts files must be in a two column format just like a normal hosts file.

server1 12.34.56.78
server2 12.45.67.89
...

3. Input commands carefully and with case sensitivity in mind.

4. When using a command string that calls a variable at the remote hosts (uses a \$ sign) be sure to double backslash before the character like so:
ps -ef | grep process | awk '{print \\\\\$2}'

5. Press Ctrl+C to abort.

