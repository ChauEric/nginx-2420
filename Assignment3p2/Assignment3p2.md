# Assignment 3 Part 2

## Firewall

#### Setting up the firewall using ufw (Uncomplicated Firewall)

The first step is to install ufw using pacman, but before we enable it, we must allow ssh access, otherwise we will be locked out of our droplet.

```
sudo pacman -S ufw
sudo ufw allow ssh
```

We can check the status of ufw with the command:

```
sudo ufw status verbose
```

Since this is the first time we are using it, it will appear as inactive, this is expected.

#### Defaults and Configuration

We will proceed with setting up defaults and configurations with the following commands:

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow from 203.0.113.0/24 to any port 22
sudo ufw deny from 203.1.113.4
```

We will limit the amount of ssh attempts to prevent malicious attempts at accessing. This will deny an incoming address if they attempt 6 initiations in 30 seconds.

```
sudo ufw limit ssh
```

We will want to allow http connections for our web server:

```
sudo ufw allow http
```

We can proceed with enabling and checking the status; however, a reboot will ensure all our changes take effect.

```
sudo systemctl reboot
```

We can now enable our firewall:

```
sudo ufw enable
```

We can check the status of ufw to ensure our settings were implemented correctly:

```
sudo ufw status verbose
```

We did it, ufw is set-up!

## Backend

### Placing backend binary on your system.

We will be using Secure File Transfer Protocol (sftp)
To achieve the backend binary, we will go to where sftp will be called, usually C:/users/[name], and create the **hello-server** file and input the provided HTML below:

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

We will then download it to our server using sftp with the following commands:

```
sftp -i .ssh/do-key YourName@DropletIP
put hello-server
exit
```

Once it is on our machine under the location **/home/${user}/hello-server**, we will relocate and rename it.

```
sudo mv hello-server /usr/local/bin/binary_backend
```

### Creating a new service file to run the backend

We will now have to make it executable and a service file to run it:

#### Making it Executable is as easy as:

```
sudo chmod u+x /usr/local/bin/binary_backend
```

#### Service File

We will create the service file

```
[Unit]
Description=Backend Service for Assignment3p2
After=network.target

[Service]
Type=Simple
#This is where the backend file is located.
ExecStart=/usr/local/bin/binary_backend
Restart=always

[Install]
WantedBy=multi-user.target
```

### Editing nginx server block, adding reverse proxy to backend.

We will configure the nginx-2420 server block to apply the supplied code.
First we will need to access it:

```
sudo vim /etc/nginx/sites-available/nginx-2420
```

We will add the following to the existing file obtained from Assignment3p1:
port 8080, 127.0.0.1:8080

```
server {
    listen 80;
    listen [::]:80;
    server_name _;
    root: /web/html/nginx-2420;
    location: index.html index.htm;

location /hey {
    proxy_pass http://127.0.0.1:8080;
}

location /echo {
    proxy_pass http://127.0.0.1:8080;
}
}
```

We can test for syntax errors or problems using:

```
sudo nginx -t
```

If there are no problems, we can restart nginx to enable the updates.

## Connection Testing

#### Testing:

```
curl http://YOUR.IP.HERE
```

Will result in a similar screen:
(Screenshot 2024-04-10 110402.png)
