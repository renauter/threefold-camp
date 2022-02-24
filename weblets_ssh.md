# SSH Key

SSH is a secure protocol used as the primary means of connecting to Linux servers remotely.
It provides a text-based interface by spawning a remote shell.
After connecting, all commands you type in your local terminal are sent to the remote server and executed there.

## Key generation with Ubuntu on WSL

Make sure SSH is installed by entering following command at the command prompt:

```sh
sudo apt install openssh-client
```

The key generation process is identical to the process on a native Linux or Ubuntu installation.
With SSH installed, run the SSH key generator by typing the following:

```sh
ssh-keygen -t rsa
```

Then choose the key name and passphrase or simply press return twice to accept the default values (`key name = id_rsa` and `no passphrase`). 
When the process has finished, the private key and the public key can be found in the `~/.ssh` directory accessible from the Ubuntu terminal.
You can also access the key from Windows file manager in the following folder:

```sh
\\wsl$\\Ubuntu\home\<username>\.ssh\
```

## Connect to remote host with SSH

With the SSH key you should be able to SSH to your account on the remote system from the computer that has your private key using the following command:

```sh
ssh username@remote_IP_host
```

If the private key you're using does not have the default name, or is not stored in the default path (not `~/.ssh/id_rsa`), you must explicitly invoke it!
On the SSH command line add the `-i` flag and the path to your private key.
For example, to invoke the private key `my_key`, stored in the `~/.ssh/keys` directory, when connecting to your account on a remote host, enter:

```sh
ssh -i ~/.ssh/keys/my_key username@remote_IP_host
```

## Enable Port 22 in Windows Firewall

The port 22 is used for Secure Shell (SSH) communication and allows remote administration access to the VM.
Sometimes it needs to be unblocked as follows:

- open Windows Firewall Advance Settings
- click on `New Rule…` under `Inbound Rules` to create a new firewall rule
- under `Rule Type` select `Port`
- under `Protocol and Ports` select `TCP`, `Specific local Ports` and enter `22`
- under `Action` select `Allow the connection`
- under `Profile` make sure to only select `Domain` and `Private`

NB: do not select `Public` unless you absolutely require a direct connection form the outside world.
This is not recommend especially for portable device (Laptop, Tablets) that connect to random Wi-fi hotspots.

- under `Name`
  - Name: `SSH Server`
  - Description: `SSH Server`
