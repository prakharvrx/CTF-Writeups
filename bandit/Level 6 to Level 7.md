Connect using SSH

After connect, I really don't where is the file so we can use this command because some of the hints are already given in the description \,

```
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size
```

So we can use this command as well to get the file `find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null` and the result is this `/var/lib/dpkg/info/bandit7.password` so using `cat` command to see the password

password : `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

