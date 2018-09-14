# resgu

Range Expect Script Generator Utility

*Important Notes* This utility requires both kornshell (aka ksh) and expect to be installed. I've tested various versions of each without issue, but make no guarantees if the version of ksh or expect that you're using do not work. 

Also, the utility will only work if you are either have passwordless authentication setup or all of the remote logins use the same password. I highly recommend the former where possible.

Synopsis:

If you don't have an enterprise level automation software available such as Ansible, but have a need to automate a repetetive task without creating an expect script everytime, then give resgu a try. Resgu is a Utility which allows for a single string to be sent via sftp or ssh to a range of ip addresses based off a specified host file. The utility generates and executes multiple expect scripts on the fly and simultaneously based off the user's interactively inputted criteria. This has been tested via SLES 9 through 11, but should also work for systems that utilize other versions of Linux as well as AIX, Cygwin or OSX (assuming you have both kornshell and expect installed). 

Initial Setup:

The resgu executable can only be executed from the users home directory. For instance if I have the user someuser1, then the user 
Setting up the Users file.

someuser1 passwordnotrequired
someuser2 passwordrequired
ansibletower passwordrequired
root passwordrequired


Usage:

When you execute the utility you will be greeted with the following information that is relevant to the setup and responses you will be providing before the ultimate execution of the expect scripts.

/------------------------------------------------------\
| Please answer the following questions appropriately. |
\------------------------------------------------------/

1. Users file must be in the following format.
user1  passwordnotrequired 
user2  passwordrequired
user3  passwordrequired

2. Hosts files must be in a two column format.

3. Input commands carefully and with case sensitivity in mind.

4. When using a command string that calls a variable at the remote hosts (uses a \$ sign) be sure to double backslash before the character like so:
ps -ef | grep process | awk '{print \\\\\$2}'

5. Press Ctrl+C to abort.

