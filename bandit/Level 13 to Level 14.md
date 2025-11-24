Connect using SSH

After Connect, first copy the `sshkey.private` file copy into your system and then use the `ssh` to connect it to bandit 14 level 

First using this command `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private` 
Then use this command `chmod 600 sshkey.private`

Then connect via SSH using this command : `ssh -i sshkey.private bandit14@bandit.overthewire.org -p 2220`

Then this level is complete you can come into the Level 14
