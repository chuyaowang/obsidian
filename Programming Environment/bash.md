# Useful Bash Commands

## Find and move

```ad-code
title: Find and Move
find . -name 'text*.txt' -exec mv '{}' collectedDir \\;
```

```ad-info

The `+` sign at the end of the `-exec` option in the `find` command is used to optimize the execution of the `mv` command. When `{}` is followed by a `+`, it tells `find` to gather the matching filenames and pass them all at once to the `mv` command, rather than executing `mv` for each file separately. This can be more efficient in terms of performance.

In this specific case, the `find` command is searching for files in the directory specified by `path_A` with names containing the substring 'AAA'. The `-exec mv -t path_B {} +` part is then responsible for moving these files to the directory specified by `path_B`. The `+` ensures that multiple filenames are passed to a single invocation of the `mv` command, which can be more efficient than invoking `mv` for each file individually.
```

## Setting proxy

https://askubuntu.com/questions/583797/how-to-set-a-proxy-for-terminal

## Remove last line

```bash
sed -i '$ d' foo.txt
```

```bash
sed -i '' -e '$ d' foo.txt
```

## Useful Bash Commands

### Getting help

Get the manual page of commands

``` sh
man command
```

### File manipulation

``` sh
ls # directory listing
ls -F # ls and shows directories, files, and executables with 
ls -al # formatted listing with hidden files
cd dir # change directory to dir
pwd # show current directory  
mkdir dir # create a directory dir  
rm file # delete file  
rm -r dir # delete directory dir  
rm -f file # force remove file  
rm -rf dir # force remove directory dir  
cp file1 file2 # copy file1 to file2  
cp -r dir1 dir2 # copy dir1 to dir2 and create dir2 if it doesn't exist  
mv file1 file2 # rename or move file1 to file2 if file2 is an existing directory, moves file1 into directory file2  
cat file # output the content of file  
vim file # edit the content of file
```

### File permission and execution

``` sh
chmod 700 file # change permissions of file to read, write and execute for the owner and no permissions for all the others
chmod 755 file # change permissions of file to read, write and execute for the owner and just execute for all the others
chmod 777 file # change permissions of file to read, write, execute for all
path/to/file # execute file or script  
./file # if in current directory
```

### Process management

``` sh
ps # display your currently active  
processes  
kill pid # kill process id pid  
killall proc # kill all processes named  
proc  
Ctrl+C # halts the current command
```

### Searching

``` sh
# Search for pattern in file
grep pattern file
ls | grep 'pattern'
```

### Networking

``` sh
ssh user@host # ssh to host as user
exit # terminate the current session
```

### Compression

``` sh
zip archive file # zip file in archive  
unzip file # unzip the file in the current directory
```

### extra: awk, job control

https://carpentries-incubator.github.io/shell-extras/

## Get storage space information

``` sh
sudo du -hx --max-depth=1 /
```

