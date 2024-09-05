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

## Too many levels of symbolic links

[Reference](https://www.baeldung.com/linux/too-many-levels-of-symlinks)

The symlink created on MacOS and Linux using `ln -s file link` can be broken if the paths are specified using relative paths. 

Essentially, the symlinks with relative sources are always relative to the folder in which the symlink is located.

Say you inside a `topDir/` have a `source.txt` and a `dir/` folder, you create the link with `ln -s source.txt dir/`. This creates a `dir/source.txt(symlink)`. However, when you use `source.txt(symlink)`, it looks for the original `source.txt` not in the `topDir/` but in `dir/`. This is because the symlink is inside `dir/` and you defined it using relative links. So what does it find? It finds itself since symlinks have the same names. This creates an infinite loop of calling itself!

Solution:
1. Use absolute paths when creating the link
2. Use relative paths, but adjust based on where the symlink is located, and make sure it points to the original correctly `ln -s ../source.txt dir/`. Here we make sure the symlink under `dir/` points to `source.txt` in `../`, which is `topDir/`, where the original `source.txt` is located.