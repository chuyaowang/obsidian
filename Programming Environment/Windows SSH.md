# Windows SSH

## Set default shell

- Default shell WSL: set registry `HKLM/Software/OpenSSH/DefaultShell to be C:\WINDOWS\System32\bash.exe`
- Default shell powershell: `New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force`

[Reference 1](https://www.hanselman.com/blog/the-easy-way-how-to-ssh-into-bash-and-wsl2-on-windows-10-from-an-external-machine)

## Port forwarding WSL -> Windows

- [Setup port forwarding from WSL to windows](https://abdus.dev/posts/fixing-wsl2-localhost-access-issue/)

## Types of port forwarding

[](https://iximiuz.com/en/posts/ssh-tunnels/)

