---
title: Django Deployment
author: Pulkit Agrawal
description: "How to Deploy Django on a VPS. We will use docker for containerisation."
pubDate: 2025-11-28
tags: ["django", "docker", "nginx", "learning in public"]
---

# Django deployment guide

In this guide we will go all the way and deploy a Django project on a VPS.

## Our Goals:

1. Start a basic Django Project
2. Containerise it using Docker
3. Push the code to Github
4. Deploy the project to the VPS

At the end of this, if we visit the domain name in our browser we should see our Django project running.

## Prerequisites:

1. Install the following on your local computer
   - Python, pip, uv, and cookiecutter,
   - Docker Desktop.
2. Get a github account
3. Buy a domain name of your choice, preferably from cloudfare.
4. Buy a basic VPS. We will use hostinger.
5. Point the domain name to the VPS.

## Broad Steps

1. Use django cookiecutter to start a new django project.

This will take us pretty far -- we will have a dockerised django project that can be deployed as is.

2. Run `docker compose up`.

This will run the django installation on your local machine which will verify that everything is in order on our local machine.

3. Push the code onto Github.
4. Set up [Github SSH](src/pages/posts/ssh-protocol.md).
5. Buy a VPS and a domain name.
6. Point the domain name to the VPS
7. Set up SSH on the VPS
8. Install git and docker on the VPS
9. Generate SSH keypair on the VPS. Provide the public key as **Deploy Keys** to the github repo. Do not provide write access.
10. Clone the repo on the VPS using the SSH access.
11. Setup environment variables in the server
12. CI/CD pipeline
   1. Go into the directory
   2. shutdown docker
   3. pull git repo
   4. docker compose again
   5. run django migrations
13. 
