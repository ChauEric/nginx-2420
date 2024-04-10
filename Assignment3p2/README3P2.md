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

We will limit the amount of ssh attempts to prevent malicious attempts of accessing. This will deny an incoming address if they attempt 6 initiations in 30 seconds.

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

We can now enable our firewall to start from boot:

```
sudo ufw enable
```

We can check the status of ufw to ensure our settings were implemented correctly.

```
sudo ufw status verbose
```

## Backend

## Connection Testing
