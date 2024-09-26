## Creating a Remote Server with DigitalOcean using doctl

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

## Introduction

In this tutorial, we will walk through the process of creating a remote server on DigitalOcean using the doctl command-line tool. We will utilize cloud-init to automate the initial configuration of the server, including user creation, package installation, and SSH key setup.

## Instructions

### Uploading Arch Linux Image 
 

1. Download the latest **Arch Linux** (https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/) ** image with the . qcow2 file extension, labeled as cloudimg. 

2. Go to Digital Ocean and click **manage**

<img src="pictures/manage.png" alt="Manage Image" style="width:50%;">












SSH keys allow you to securley connect to your Droplet, and they are safer than passwords since the private key remains on your computer.