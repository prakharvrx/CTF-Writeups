Connect with SSH

username : bandit1
host : bandit.labs.overthewire.org
port : 2220
password : ``ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

After connect, using `pwd` to see the current directory and go back to the directory `/home` by using the command `cd ..` and go to the directory `bandit1` by using this command `cd bandit1`  you can see the dash file `-`  so using this command to see the file content `cat < -` 

Well Using this command `cat < - ` to get the password for level 2 

We can use the command `./-` but we don't have permission so we can using this `cat < -` instead of the `./-` 

password : `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
