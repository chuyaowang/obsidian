# MS Word Add-in

[Source](https://learn.microsoft.com/en-us/office/dev/add-ins/tutorials/word-tutorial)
## Initialize the project

### Prerequisites

- [Node.js](https://nodejs.org/) (the latest [LTS](https://nodejs.org/en/about/previous-releases) version).
    
- The latest version of [Yeoman](https://github.com/yeoman/yo) and the [Yeoman generator for Office Add-ins](https://learn.microsoft.com/en-us/office/dev/add-ins/develop/yeoman-generator-overview). To install these tools globally, run the following command via the command prompt.

```
 npm install -g yo generator-office
```

### Create the project

``` 
yo office
```

### Run the dev-server

> This will start the web app in the word app installed on macOS.

```
npm run dev-server
npm start
```
## [Hello World Example](https://github.com/OfficeDev/Office-Add-in-samples/tree/main/Samples/hello-world/word-hello-world)

- This is currently in the `~/R Projects/My Office Add-in` directory.

- An app must contain two parts: the [manifest](https://learn.microsoft.com/en-us/office/dev/add-ins/develop/add-in-manifests) and the web app.

> [!note] Manifest
> A manifest file enables an Office Add-in to do the following:
> 
> - Describe itself by providing an ID, version, description, display name, and default locale.
>     
> - Specify the images used for branding the add-in and iconography used for [add-in commands](https://learn.microsoft.com/en-us/office/dev/add-ins/design/add-in-commands) in the Office app ribbon.
>     
> - Specify how the add-in integrates with Office, including any custom UI, such as ribbon buttons the add-in creates.
>     
> - Specify the requested default dimensions for content add-ins, and requested height for Outlook add-ins.
>     
> - Declare permissions that the Office Add-in requires, such as reading or writing to the document.

> [!note] Web App
> 
> The web app contains the html code and javascript code that constitutes the body of the web app.

## [Tutorial](https://learn.microsoft.com/en-us/office/dev/add-ins/tutorials/word-tutorial)



