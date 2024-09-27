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

3. Type ```mkdir .ssh``` 

(image)

4. Type ```ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"``` and **enter** to generate a new SSH key pair

NOTE: Change "your email address" to your email of choice and you can change key name, for example hello-key

5. Press **enter** and type a passphrase or press **enter** for no passphrase

(image)

### Adding public key to your DigitalOcean Account

1. Copy and paste the following commands to copy your SSH key

```pbcopy < ~/.ssh/do-key.pub``` 

NOTE: Replace "do-key" with the name of your SSH key.

2. Go to DigitalOcean and **click** settings. 

(image)

3. Click security and **add SSH key** 

4. Paste the copied key in the content box then enter a SSH key name

(image)

NOTE: If error message "SSH key content must be a valid SSH key" enter backspace to troubleshoot this problem. 

5. Click **Add SSH Key** 

### Installing DOCTL 

1. Open your Terminal or Command Prompt

2. Install Homebrew on your MacOs

3. Once installed, Type and run the following **command**

```brew install doctl``` 

(image)

4.Type ```doctl version``` once installed to verify the installation

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














