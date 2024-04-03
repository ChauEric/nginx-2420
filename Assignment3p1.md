# Running a server using nginx

## Making the directory

To ensure we the work we do is organized, we must first create the directory that will act as our project root.

To do so, we will use the following command:

```
mkdir -p /web/html/nginx-2420
```

The **mkdir** the _make directory_ command creates the directory we will be working in and **-p** is an option for mkdir allows us to nest the subsequent directories within the _parent_ directory.

## Software Requirements

To work with nginx and made subsequent changes to the index.html file, we must download the necessary software.

```
sudo pacman -S nginx vim
sudo pacman -Syu
```

**sudo** is a command that gives the user the **superuser do** security privilege to make changes.
**pacman** is the _package manager_ used by the Arch Linux distro. **-S** is the command to install one or more packages and any dependencies

**nginx** - high-performance HTTP web server (https://wiki.archlinux.org/title/Nginx)
**vim** - terminal text editor. (https://wiki.archlinux.org/title/Vim)

_Additionally, we will run -Syu to update all installed packages_

Navigate to the user's nginx default location file. It is assumed that you use the default location for documents.

```
cd /usr/share/nginx/html
```

**cd** is the _change directory_ command and will move you to the folder specified in the path.

Once in this directory, we will edit the existing example index.html file.

```
sudo vim index.html
```

Delete the existing content and replace with the following snippet:

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>
```

If that is not the case, substitute your path instead.
