# Making File Links

File links are advanced shortcuts that point to files or folders, redirecting applications to access them as if they were in a different location.

## Windows

- Soft link (symlink): redirect to the location where files are stored. A symlink can refer to network volumes.
- Hard link: make it appear as though the file exists at the location of the symbolic link. A hard link cannot be created for a folder. A hard link also cannot be created across volumes.
- Junction: similar to hard links, but for directories.

````ad-code
title: Choose One

```console
mklink /D <link> <target>
mklink /H <link> <target>
mklink /J <link> <target>
```

- link refers to the link created
- target refers to the original file/folder

````
^windowslink

## MacOS

- Symlink: can link to files or folders and span volumes. If the linked file/folder is removed, the link breaks.
- Hard link: link to files. Changes to the link is also reflected in the original file. Hard links cannot be created for folders and cannot be across volumes.

````ad-code
title:Choose One

```console
ln -s <file> <link>
ln <file> <link>
```

- file refers to the original file/folder
- link refers to the link created
- yes it's the opposite of windows

````
^macoslink

- To remove the link, just `rm` it.
