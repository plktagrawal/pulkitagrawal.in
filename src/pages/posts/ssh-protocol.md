---
title: SSH Protocol
author: Pulkit Agrawal
description: "What is SSH Protocol and how to set it up (for GitHub as an example)"
pubDate: 2025-11-28
tags: ["ssh", "learning in public"]
---

# Secure Shell Protocol (SSH)

SSH provides a **secure channel** over an unsecured network. Its most common use case is to access (login) into a remote server without a password.

## How it works

SSH uses public-key cryptography to authenticate the remote computer.

You generate two keys:

1. A public key
2. A private key

The public key can create a puzzle (or challenge) that can only be solved by the private key.

You share the public key with the server (or even the whole world if desired; which is why it is called the _public_ key).

Whenever a client (say, your laptop) tries to access the server (say, Github), the server creates a new challenge using the public key and sends it back. The client can solve the challenge only if it has the private key. Sending the correct answer to the server instantly grants access.

## Benefits

The other alternative is to have a password mechanism. But a password is same everytime the server is accessed. If someone can intercept the password, they can gain access to the server by reusing it.

In SSH Protocol, the server sends a new challenge everytime and the corresponding answer is also unique. Even if the answer is intercepted, the chance of someone being able to reverse-engineer the private key from the answer is minimal.

## How to setup SSH

The steps are as follows:

1. Generate the Key pair on your local machine
2. Add the SSH key to the SSH agent
3. Copy the public key
4. Provide the public key to the server

### On MacOS

1. Generate the Key pair with:

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter to accept the default path: ~/.ssh/id_ed25519.

Once the key is generated you will see a message saying that the key is saved and that message will also show the path at which the key is saved.

2. Add the SSH key to the SSH agent

```sh
eval "$(ssh-agent -s)"
```

3. Copy the public key
   You can see the public key with the cat command. Use the path that was shown to you in step 1.

```sh
cat <path-to-the-public-key>
```

```sh
pbcopy < ~/.ssh/id_ed25519.pub
```

4. Provide the public key to the server

<strong>Let's use Github as an example.</strong><br />
Login to your account. Then setting > SSH and GPG Keys > New SSH Key

Provide a name to identify the client. And paste the result of step 3. Hit save and you are done.

<strong>Hostinger VPS</strong><br />
Provide the same public key to Hostinger as well.

# How to log in to a server

If you want to log in to Hostinger now, just say:

```sh
ssh root@<ip-of-your-server>
```

# References

Detailed steps are here:
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
