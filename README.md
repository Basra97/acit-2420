## Creating a Remote Server with DigitalOcean using doctl

### Table of Contents

1. Introduction
2. Prerequisites
3. Step 1: Create SSH Keys
4. Step 2: Install and Configure doctl
5. Step 3: Create a Custom Arch Linux Image
6. Step 4: Create a Droplet with doctl
7. Step 5: Connect to Your Droplet
8. Conclusion
9. References

### Introduction

In this tutorial, we will walk through the process of creating a remote server (Droplet) on DigitalOcean using the doctl command-line tool. We will utilize cloud-init to automate the initial configuration of the server, including user creation, package installation, and SSH key setup.
