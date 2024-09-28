## Creating a Remote Server with DigitalOcean using doctl

NOTE: Instructions for MacOs Users

## Table of Contents

1. Introduction
2. Prerequisites
3. Step 1: Uploading Arch Linux Image
4. Step 2: Create SSH Keys
5. Step 3: Install and Configure doctl
6. Step 4: Create a Custom Arch Linux Image
7. Step 5: Create a Droplet with doctl
8. Step 6: Connect to Your Droplet
9. Conclusion
10. References

redo above after finishing

Use <br>

## Introduction

In this tutorial, we will walk through the process of creating a remote server on DigitalOcean using the doctl command-line tool. We will utilize cloud-init to automate the initial configuration of the server, including user creation, package installation, and SSH key setup.

## Instructions

### Uploading Arch Linux Image 
 

1. Download the latest **Arch Linux** (https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/) image with the .qcow2 file extension, labeled as cloudimg. 

<img src="pictures/arch.png" alt="Manage Image" style="width:50%;">

2. Go to Digital Ocean and click **manage**

<img src="pictures/manage.png" alt="Manage Image" style="width:50%;">

3. Click **Backups & Snapshots** on the dropdown menu

<img src="pictures/Untitled document (3).png" alt="Manage Image" style="width:50%;">

4. Click **Custom Images**

5. Click **Upload Images** and select Arch Linux Image and open the file

6. Click on **distribution** and select Arch Linux

<img src="pictures/Untitled document (4).png" alt="Manage Image" style="width:50%;">

7. Select your closest region

<img src="pictures/Screenshot 2024-09-25 at 10.36.18 PM.png" alt="Manage Image" style="width:50%;">

8. **Click** Upload Image

### Creating SSH Keys

SSH keys allow you to securley connect to your Droplet, and they are safer than passwords since the private key remains on your computer.

1. Open your Terminal or Command Prompt

2. Type ```cd``` to see your current directory

3. Type ```mkdir .ssh``` and ```cd``` into .ssh

(image)

4. Type ```ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"``` and **enter** to generate a new SSH key pair

NOTE: Change "your email address" to your email of choice and you can change key name, for example hello-key

5. Press **enter** and type a passphrase or press **enter** for no passphrase

6. Type cd .ssh then use ls to confirm your authorized keys

(image)

### Installing DOCTL 

1. Open your Terminal or Command Prompt

2. Install Homebrew on your MacOs by copying the following command

``` /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

3. Once installed, Type and run the following **command**

```
brew install doctl
``` 

(image)

4.Type ```doctl version``` once installed to verify the installation

![Upload Image](./Pictures/Select%20your%20closes%20region%20and%20Click%20Upload%20Image.jpg)


### Adding public key to your DigitalOcean Account using doctl

1. Copy and paste the following commands to add SSH key to DigitalOcean 

```
doctl compute ssh-key create "My SSH Key" --public-key "$(cat ~/.ssh/do-key.pub)"

``` 
2. Press Enter 

(image)

NOTE: Replace "do-key" with the name of your SSH key and "My SSH Key" with your preferred name

3. Go to DigitalOcean and **click** settings. 

(image)

3. Click security and see if your key is uplodaed

(image)

### Creating an API Token

1. Click API on the left hand side of the Menu on DigitalOcean

(image)

2. Click **Generate New Token**

3. Type a **Token Name**, and give it **full access** then click **Generate Token**

(image)

4. Copy and Paste the **token** in a secure storage, file or server. 

NOTE: A **Generated Token** is only shown once.

### Using The API Token to Grant access to doctl

1. Open terminal or command prompt

2. Type the following command 

```doctl auth init --context NAME```

NOTE: Change **NAME** to something appropiate

3. Copy and Paste your generated token into the terminal

(image)

4. Press Enter and wait for a green checkmark.

Example Validating token... ✔

(image)

5. Run ```doctl account get``` to validate that doctl is working successfully

(image)

### Configuration of The Cloud Init File 

**install neovim** 

``` brew install neovim
```

1. Type the following command to create a file

```nvim cloud-config.yaml```

2. Copy and Paste the following content into the **file**, then pres i for "insert mode"
#
#cloud-config
users:
  - name: example-user
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh_authorized_keys:
      - <your public SSH Key>
disable_root: true
packages:
  - nginx
runcmd:
  - 'export PUBLIC_IPV4=$(curl -s http://169.254.169.254/metadata/v1/interfaces/public/0/ipv4/address)'
  - 'echo Droplet: $(hostname), IP Address: $PUBLIC_IPV4 > /var/www/html/index.html'

3. Change name to your name

4. Change gh:<your public SSH Key> with your SSH Key

NOTE: Remove <>

(image)

5. Press esc to exit Insert Mode and type :wq to save and exit nvim

(image)

go to home and see if the yaml file is made

### Deployment of Droplet with Cloud-init

1. Open Terminal 

2. Type or Copy the following command, then locate your key ID

``` doctl compute ssh-key list ```

3. Copy and Paste the following into the terminal

4. Use the command below to check list of image

```doctl compute image list-user```

5. Run the followig command to create your droplet

``` 
doctl compute droplet create --image 165064169 --size s-1vcpu-1gb --region sfo3 --ssh-keys < git-user > --user-data-file < path-to-your-cloud-init-file > --wait first-droplet 
 
```
NOTE: Change < git-user > with your ID number from step 2

Replace  < path-to-your-cloud-init-file > to the path of your cloud-config.yaml file

(image)

6. Press Enter 

NOTE: This command may take a minute

(image)

7. Type the following command to verify if it worked

doctl compute droplet list

then copy the following command to connect to your droplet

``` ssh -i < /path/to/private-key > username@your-droplet-ip ```

fix problem above, fixed


NOTE: if ``` [Example@first-droplet ~]$ ``` appears you have successfully connected to your droplet





add public key to digitalocean using doctl


use doctl to add arch linux file to digital ocean














