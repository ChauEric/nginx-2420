# Running a server using nginx

## Making the directory

To ensure we the work we do is organized, we must first create the directory that will act as our project root.

To do so, we will use the following command:

```
mkdir -p /web/html/nginx-2420
```

The **mkdir** command creates a directory and **-p** is an option for mkdir allows us to nest the subsequent directories within it.

## Software Requirements

To work with nginx and create subsequent changes, we must download the necessary software.

```
sudo pacman -S nginx vim
sudo pacman -Syu
```

**sudo** is a command that gives the user the **superuser do** security privilege to make changes.
**pacman** is the package manager used by the Arch Linux distro. _-S_ is the command to install one or more packages and any dependencies
_Additionally, we will run -Syu to update all installed packages_
