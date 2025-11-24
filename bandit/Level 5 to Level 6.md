Connect using SSH

After connect, go to the directory `/inhere` and you can see the lot of many directory but in this challenge there's a hint which is written in the description of that challenge is file isn't executable and their size is `1033` bytes so we can use this command to find out that file using this command  `find . -type f -size 1033c ! -executable -exec file '{}' \;` so it can gives this result `./maybehere07/.file2: ASCII text, with very long lines (1000)`
so using `cat` command to see the content of file `file2` 

password : `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`