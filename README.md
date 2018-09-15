# resgu

Range Expect Script Generator Utility
                                                                                                                                                                                                                                                                  

Important Notes: 

This is an extremely powerful utility with very constructive or destructive capabilites depending on who's using it! Upon execution of the utility make sure that you quadrupal check your answers to the interactive prompts.

This utility requires both kornshell (aka ksh) and expect to be installed. I've tested various versions of each without issue, but make no guarantees if the version of ksh or expect that you're using cause the utility to fail. 

Also, the utility will only be able to reach your target hosts if you either have passwordless authentication setup for all target hosts or all of the target hosts logins use the same password. I highly recommend the former where possible.

Any user can use the utility (sudo not needed so only give this to users that can be trusted).

Make sure your Users and hosts files do not have any blank lines in them.
                                                                                                                                                                                                                                                                         
Synopsis:

If you don't have an enterprise level automation software available such as Ansible, but have a need to automate a repetetive task to tens, hundreds or even thoughands of servers without creating an expect script everytime you have a new task to do, then give resgu a try. Resgu is a utility which allows for a single string to be sent via sftp or ssh to a range of ip addresses based off a specified host file (sorry ftp is not included due to security issues with the protocol). The utility generates and executes multiple expect scripts on the fly and simultaneously based off the user's interactively inputted criteria. This has been tested via SLES 9 through 11, but should also work for systems that utilize other versions of Linux as well as AIX, Cygwin or OSX (assuming you have both kornshell and expect installed). The utility is written in kornshell and expect so feel free to make your own alterations.
                                                                                                                                                                                                                                                                             
Initial Setup:

There is a very small amount of setup that needs to be done to get the utility to work properly.

1. Placing resgu and the required files in the appropriate directory

The resgu executable can only be executed from a users home/user/resgu directory. For instance if I'm logging into the central server as the user "someuser1", then the resgu executable and it's required files must be in the "/home/someuser1/resgu" directory.

2. Setting up the "Users" file

A file called "Users" must be placed in the directory where resgu executable is. Resgu uses this to tell if the remote user is already setup up with passwordless authentication or not. If not you will be prompted to enter a password. First column is the name of the user and the second column should be set to either passwordnotrequired or passwordrequired accordingly.

someuser1 passwordnotrequired                                                                                                   
someuser2 passwordrequired                                                                                                       
ansibletower passwordrequired                                                                                                   
root passwordrequired                                                                                                           

3. Setting up a single or multiple hosts files

One or more hosts files named whatever you'd like must be placed in the directory where the resgu executable is. Resgu uses this to connect to the remote hosts via a range that you select interactively upon execution of the utility. Hosts files must be in a two column format just like a normal hosts file. 

server1 12.34.56.78                                                                                                             
server2 12.45.67.89                                                                                                             
server3 13.56.78.89
                                                                                                                                                                                                                                                                     
Usage:

From your user's home/resgu directory type the below command to start the utility.                                             
./resgu

When you execute the utility you will be greeted with the following warning information that is relevant to the setup and responses you will be providing before the ultimate execution of the expect scripts.

Please answer the following questions appropriately.

1. Users file must be in the following format.
user1  passwordnotrequired 
user2  passwordrequired
user3  passwordrequired

2. Hosts files must be in a two column format.

3. Input commands carefully and with case sensitivity in mind.

4. When using a command string that calls a variable at the remote hosts (uses a \$ sign) be sure to double backslash before the character like so:
ps -ef | grep process | awk '{print \\$2}'

5. Press Ctrl+C to abort.
                                                                                                                                                                                                                                                                  
Interactive prompts:

1. First enter the name of one of your hosts files.                                                                             
testhostsfile

2. Next enter the first host of your range in your selected hosts file.                                                         
host1

3. Next enter the last host of your range in your selected hosts file.                                                         
host1000

4. Next enter the username of your desired remote login.                                                                        
someuser1

5. Next enter the password for the user if the user requires a password to login rather than using passwordless authentication (password will not appear on the screen).

6. Next select 1 for sftp or 2 for ssh.                                                                                                                                
2

7. Next enter the command to be executed.                                                                                       
put somefile somewhere

8. Select between 1 and 23 to choose the length of your timeout in seconds (example is for 30 minutes).                                                    
2

9. Select between 1 and 7 to choose the amount of connections to be established simultaneously.                                  
7

Logging: 

To check the progress of the utility you can open a new command line interface and view the templog files under the /tmp directory. How many templogs there are depends on how many simultaneous connections you chose to have. If there are 7 then there will be a file at /tmp/templog1, /tmp/templog2 and so on until /tmp/temlog7.

Final file
Once the utility has finished, then a log file while be generated in the same directory as where the resgu executable was. The log file will be called job(DATE).log. For example if today is December 25th 2018, then the log file will be called job12122018.log. I highly recommend that you check out the log file after execution to make sure the utility does exactly what you wanted.
