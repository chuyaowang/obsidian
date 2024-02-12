# WSL Usage Notes

## Restart WSL

> [!note] Steps
> 
> 1. Open **Terminal**.
> 2. Enter `wsl --shutdown`. Press *Enter*. If the command hangs, skip to step 5.
> 3. Enter `wsl`. Press *Enter*.
> 4. Enter the password: metametameta.
> 
> 1. Press *Ctrl+C* to end the previous command.
> 2. Enter `tasklist /svc /fi "imagename eq svchost.exe" | findstr LxssManager`
> 3. A number(**PID**) will be returned.
> 4. Open **Task Manager**. Go to *Details*.
> 5. Scroll down to find *svchost.exe* with the **PID** matching the number in step 7.
> 6. Right click on the *svchost.exe*. Select *End Process Tree*.
> 7. Enter `wsl`. Press *Enter*.
> 8. Enter the password: metametameta.
^restart-wsl

## Export Data to Another Drive

````ad-code

``` bash
wsl --shuwdown
wsl --list
wsl --export distro-name <target dir>
wsl --unregister distro-name
wsl --import <new dir> <target dir> --version 2
```
Ex.
\<target dir>: D:/wsl-data.tar
\<new dir>: D:/wsl-data/

````
