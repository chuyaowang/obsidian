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
