# Linux: List, Set and Change File Permissions

To list the permissions of all files in a directory you use `ls -l`. Files and directories can only be modified by the owner, unless the sudo root user. Linux also has groups to which the files or directories can be assigned. To change the assignation to a different group you use `chgrp group_name file/directory`. You can only change the groups that the current user is part of; to see the groups you use `groups`. You can also change ownership of a file or dir to another user with the command `sudo chown user file/directory`. This can only be done by the sudo user. You can change both user and group ownership with this command, but you must use the following syntax: `sudo chown user:group_name file/directory`. 

`ls -l` also shows the permissions and caregory of the files. The categories are d (directory), - (reg file), c (character device), l (link), s (socket file), p (pipe), b (block device). Next nine characters show permissions `rwxrwxrwx`, exh set of `rwx` corresponds to user (u), group (g) and others (o). The meaning of these is slightly different if it's a file or a directory; r means read permission, w write permission and x execute permission. If there is a - (dash) there is no permission. For files this `rwx` referrs to modyifing the contents of the file; whereas for directories it applies to the directory itself, files and subdirectories inside. r means you can see it with `ls`, w means you can write to this directory; i.e. adding or creating files/subdirs in this directory; x means we can execute in the directories; i.e. using `cd` to enter the directory. 

Permissions are read by Linux from left to right, so if the group has permissions, but the user that owns the file and belongs to the group doesn't, the permissions related to the user apply. If the user is not the owner, but part of the group, group permissions apply. If it belongs to neither, other permissions apply. To change permissions of files you use `chmod permissions file/directory`. To add permissions you use `u+wrx` for user, `g+rwx` for group and `o+rwx` for others. To remove permissions you do the same, but instead of + you use -. To set the exact permissions you replace the + or - with =. If you omit all letters in this it would remove all the permission, just like `o-rwx`. You can join all user, group and other permissions by using commas: `chmod u+rw,g=r,o=`. You can also use octal permissions. 

The `stat` command also shouw permissions, but with the Octal value at the begining representing the groups. These are calculated by binary representation, which when converted each part into decimals gives some values. Another approach would be the octal table, in which each permission has a value 4 for r, 2 for w 1 for x. Once identified, we can use the number with the `chmod` to modify permissions: `chmod 640 file/dir`.

## Pagers and Vim

Pagers are programs made to read files and navigate through pages. There are two, less or more. To access them you just type `less file`. To know if pager, look at bottom left for highlighted name of file. To search the pager you can use arrow keys, and use / to search `/search`, to move to next instance you press n key, togo back you use shift+n keys. If you want to stop case sensitivity you must use `-i`. To exit, just press q. more is accessed the same and will show more at the bottom, you move with spacebar and to leave you use 'q'.

Vim text editor is accessed through `vim`. This text editor is mode sensitive, so in order to write you must press the 'i' key and when INSERT appears, you can write. With `esc` you go back to default mode. To search in Vim you use /+search. To make the search case insensitive you use `/search\c`. You can also go to line number by typing ':' followed by line number. To copy line in command mode, you type 'yy' and paste with 'p'. You can also cut a line with 'dd'. To leave you save with `:w` to write, to quit and save `:wq`, to quit without saving `:q?`. 

# Searching files in Linux using 'grep'

`grep search file` is used to search inside a file. this search is case sensitive, but you can use `-i` to ignore case sensitivity after `grep`. We can also search for all files that exist under a dir and subdir with `-r` (recursive); instead of specifying file you specify directory. You can also combine that option with ignoring case sensitivity as `-ir`. To search through system files it's imperative to use `sudo`. We can also invert the search, so we can search for example for lines or files that do not have something using the `-vi` option. If we want to match only the expression being searched you can use the `-wi` option. Grep shows the entire line, but if we only want the result we use the `-o` option. You can manipulate strings with `sed`. 

# Using Regular Expressions + Grep

What if you need to extract IP addresses from 10000 logs? We can use regular expressions to search trough all documents, which is the same as a symbolic representation of what we want. In Linux the regex operators are:

- `^`: begins with -> placed at beginning of pattern
- `$`: ends with -> placed at the end of pattern
- `.`: match any ONE character -> if you need a '.' use '\.'
- `*`: match the previous ellemnt 0 or more times -> can be paired up with other operators '/.*/'
- `\+`: match the previous element 1 or more times -> must be used in it's scaped form

**If you want to avoid escaping operators you can use `grep -Er '0+'` or `egrep`. Common practice is to always use this last one.** 

- `{}`: previous elemnt can exist in the contained element this many times. -> use with comamas at start to find at least x amount or at the end for at most. Can be a range too.
- `?`: make the previous element optional 
- `|`: match one thing or the other x|y -> can be combined to search for variations `egrep -ir 'enabled?|disabled?' /etc/`
- `[]`: range or sets [a-z],[0-9],[A-Z],[abz954] -> searching 'cat' `egrep -r 'c[au]t' /etc/` -> they can be wide or specific at the same time. -> after /dev/ match any characters, which migth en with numbers: `egrep -r '/dev/[a-z]*[0-9]?' /etc/`.
- `()`: subexpressions -> wrap construc in parenthesis so that * applies to the whole construct: `egrep -r '/dev/(([a-z]|[A-Z])*[0-9]?)*' /etc/`
- `[^]`: negated ranges or sets (look for http not https) -> `http[^s]`

**You can use regex in many more programs including Python!**
