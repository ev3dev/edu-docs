# Remote Access to Robot Controller Using Secure Shell (SSH)

* Enabling Networking on the Target
* Setting Up SSH Access
* Using Public Key Authentication
* Downloading/copying Programs to the Robot Controller

## Enabling Networking on the Target

See the topic on [Networking](http://www.ev3dev.org/docs/networking/) for more information on how to enable network access on the Robot Controller.

## Setting up SSH Access

Secure Shell (SSH) is the recommended way to connect to the Robot Controller from the Host. The most commonly used SSH package is OpenSSH, which is supported by all the major OSes. Alternatively, Putty is available on Windows as a SSH client.

> The default Developer's Firmware from LEGO uses `telnet` for access to the EV3 running `D` version firmware. Resist all temptations to install or use `telnet` and `telnetd` on ev3dev, as it is an obsolete remote access protocol which transmits *EVERYTHING* you type in cleartext over the network link. You should excise any usage of `telnet` from your repertoire of command line tools as it is the road to grief and [security compromises](https://translate.google.com/translate?sl=auto&tl=en&js=y&prev=_t&hl=en&ie=UTF-8&u=http%3A%2F%2Fwww.heise.de%2Fsecurity%2Fartikel%2FAnalysiert-Lego-Mindstorms-fuer-Cyber-Angriffe-missbraucht-3055305.html&edit-text=&act=url).

The basic way of connecting to the Robot Controller is to specify the username and host information to the SSH client:
```
$ ssh robot@<robotcontroller> 
[where <robotcontroller> is either the hostname or IP address of the Robot Controller]
```

e.g., 

```
$ ssh robot@192.168.2.2
```

The first time you connect to the Robot Controller, it might complain that it is an unknown host, or else the cached Robot Controller credentials does not match.
If it is indeed the first time you're connecting to the particular controller, you can accept the prompt. If it complains about non-matching credentials, you may need to remove the old cached entry manually.

After the connection is established, SSH will present the login prompt for the password.
You can then login to the ev3dev environment using the appropriate password. (the default password is `maker`).

> See [Connecting to Ev3dev Using SSH](http://www.ev3dev.org/docs/tutorials/connecting-to-ev3dev-with-ssh/) for more information.
>

If this is your personal EV3, it is of course prudent to change the password to something other than the default. 

>In a Lab environment, your instructor may advise you to use the default password to avoid unnecessary problems logging into the Robot Controller.

Changing passwords on ev3dev is the same as on any Linux distribution:

```
$ passwd
```

## Using Public Key Authentication

Once you've mastered logging in using SSH, and is frustrated with the constant need to type in your password at the login prompt, you can explore the use of Public Key Authentication for SSH login.

[Creating SSH Login Keys](https://www.ssh.com/ssh/keygen/)

> Remember to copy the SSH Login Public Key to the server. `ssh-copy-id` is one way of doing so.
>
> The advantage of using Public Key Authentication is that you don't need to transmit your password over the network link (even if it is encrypted) when logging in. In addition, the security of using Public Key Authentication is much better since the credentials are much longer than the typical user password.

You should protect the SSH Login Key with a passphrase (specified during the Login Key generation step). Most SSH client software can automatically unlock the SSH Login Key from your Host OS environment using `ssh-agent` , so that you don't even have to manually type in your passphrase to unlock the SSH Login Key each time. This make logging in to the Robot Controller a single step by just issuing the ssh command with the appropriate username and hostname/ip address.
