# Notes on Working with files and Directories in Linux

To see files and directories in current directory you use "ls". However, some docs start with a "."; these are hidden files, which can be seen using "ls -a". To see other files and directories in a different one, you use "ls /dir/dir/dir". If we want more details we can use "ls -l", to have a long list format with permissions, etc. You can also combine -a and -l to apply the same long format to include even hidden files as "ls -a -l" or "ls -al". There's also "-h", which shows human readable sizes. You can combine all three as "ls -alh".

Linux organizes files and dirs in a Fylesystem tree. The root is on top, and the branches descend from it. The symbol for root is "/". Under root, there are other subdirectories such as home or var, which also have subdirectories. To navigate this tree you can use directory or file paths, which can be written as absolute (starting on root) "/home/godo/etc/file(.pdf)", or as relative. To understand this one, you first have to know the working directory with "pwd" (print working directory"). In CLI you are always in a directory, and every user starts at it's own directory. Users start at "/home/user" while root starts at "/root" (super user or admin). To navigate between directories you use cd (change directory) + absolute path, or with ".." to go one directory up. 

With relative paths we can move in three ways:
1. locations under current directory (/documents/Invoice.pdf)
2. locations under current directory (invoice.pdf)
3. locations above current directory (../Invoice.pdf) -> can be used multiple times!

You can return to previous directory with "cd -", or you can use just "cd" to go back to home. 

To create a file in current directory you use "touch file.txt", and to create a file in another directory you use "touch /home/user/file.txt". We could also use a relative path if we are in home, for example, as such "touch ../userfile.txt". After command, you can use any path you want.

To create a new dir you use "mkdir Receipts" (make directory). You can also add flag "-p" to create also the necessary parent directories.

To copy a file you use "cp [source] [destination]". For example, cp file.txt Receipts/ (the final slah is good practice to distinguish files and directories". This command can also be used to copy and rename files as such "cp file.txt Receipts/filecopy.txt". To copy a directory and its contents to another you can use the command flag "-r", which tell the command to copy recursively; that is the directory with everything in it: "cp -r [source] [destination]". An example would be a backup of a full directory: "cp -r Receipts/ BackupReceipts/". The name must be unique to work. To preserve all of a file's attributes when copying, you can use the flag "-p" as such "cp -p [src] [dst]".

To move a file from one location to another you use the command "mv [source] [destination]" (move) command: "mv file.txt Receipts/". You can also rename files and directories with this command as such "mv file.txt oldfile.txt" and "mv Receipts/ oldreceipts/". Use of -r is not necessary, because mv does that too. 

To delete a file you can use "rm" (remove) as such "rm oldfile.txt". You can also delete directories by adding the recursive -r flag as such "rm -r oldreceipts/".

## Create and manage hard and soft links

### Hardlinks

First, some basics of filesystems. You can create a filepath with "echo". For example "echo 'Picture of doggo' > Pictures/doggo.jpg". There is a command that shows interesting things about files and directories, and that is the "stat". This showcases Inodes, which help keep track of data. Each file points to an inode, and each inode points to all the blocks of data that it requires. The command "stat" also shows links of the file, this is the number of hard links to each file or directory. To explain this, when you create a file in Linux, the OS takes all the file's data (or blocks of data scattered in the disk) for it and groups it togheter in an specific unique inode that remebers their location on the disk, and `hard links` it to the file to be able to access the data. So, `file -> inode -> blocks of data`. 

Why would a file or directory have more than 1 hardlink? You could hardlink an inode to another user's directory instead of using "cp", to avoid storing data twice in the disk, which could be a problem with large amount of data. The command to hardlink thusly is "ln path_to_target_file path_to_link_file". However, hardlinks can only be used for files, and files in the same filesystem. This process requires the  to have the necessary permissions to create file at destination. Also, all users involved must have the required permissions to access file. This could mean adding the users to same group with "useradd -a -G grooup user", and then using "chmod 660 /home/.../file.png" to change permissions on the file.

### Soft Links

`Soft links` are similars to windows desktop shortcuts. Indeed, while `hardlinks` point to `inodes`, `soft links` are files that point to paths to the file. The syntax of creating a soft or symbolic link is "ln -s path_to_target_file path_to_link_file". When "ls -l" we might get a large file path with permissions, etc; but if we only want to read link, we use "readlink dooggo_shortcut.png" to get the path. Permissions of symbolic links do not matter, as the permissions of the destination file apply. Broken links will be highlighted in red with "ls -l" command, you could solve it by navigating to a relevant directory and using a relative path with "ln -s". Contrary to hardlinks, you can soft linkf files and directories, even in different filesystems. 
