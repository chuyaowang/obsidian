# FTP

## Establishing an FTP connection

First use `ftp` to connect to the file server.

> [!code]
> ``` console
> ftp domain.com
> 
> ftp 192.168.0.1
> 
> ftp user@ftpdomain.com
> ```

## Authenticate

Enter username and password.

> [!code]
> ```console
> Name: your-name
> Password: password
> ```

## Operating with directories


> [!code]
> ```console
> ls
> mkdir
> cd
> ```

## Downloading files

Set up local download directory.
> [!code]
> ```console
> lcd ~/directory
> ```

Download.
> [!code]
> ```console
> get file
> mget *.xls
> ```

## Uploading files

> [!code]
> ```console
> put file
> put ~/file
> mput *.xls
> ```
