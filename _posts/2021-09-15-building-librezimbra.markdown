---
layout: post
title:  "building LibreZimbra"
date:   2021-09-15 15:45:12 +0200
categories: librezimbra update
---
Building LibreZimbra is currently still a bit complicated :(

Prerequisites:
- git
- docker
- python
- 10..15 GB free space


First step is cloning the [librezimbra main repo](https://github.com/LibreZimbra/librezimbra)
which servers as the central workspace. It contains a bunch of scripts / tools for managing
the workspace, eg. cloning all the individual git repos, starting the build, etc.


In this workspace you'll find several scripts, the first to be called is ''clone-all'. This
will take a while to clone, eating up about 3 GBs. (on build it will grow to round 8GB).
The cloned git repos are found in the ''pkg/'' subdirectory.


Note that once cloned, the git repos will NOT be pulled/merged automatically - so you can
make your local changes at will.


Next step is creating a build container. That's done by ''start-build-container'' - on first
run it will build a container image for the build containers. Note that the image is customized
for your user account (eg. matching up UIDs etc). Once you're in, you'll find yourself under
the ''build'' user, which is mapped to same UID as your user on the host. The workspace directory
(which you cloned above) is mounted to /home/build/src inside the container. And the ~/.ssh
directory is mapped to your host user's ~/.ssh.


This website is managed via the jekyll tool and living in the librezimbra.github.io repo.
A local webserver for serving this site directly from local git source can be fired up via
the ''run-server'' script inside this repo. It will listen to port 4000, which is also mapped
to the same port on the host.

Feel free to leave some feedback (eg. tickets) or join the [Telegram group](https://t.me/librezimbra).


Hint: if you messed up one of the git repos in ''pkg/'', and no local changes you wanna keep,
you can just remove the broken repo and run the ''clone-all'' script for toplevel directory again.
The missing repo will automatically be cloned again.
