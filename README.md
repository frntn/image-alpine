# Alpine Linux image on Scaleway

[![Build Status](https://travis-ci.org/scaleway/image-alpine.svg?branch=master)](https://travis-ci.org/scaleway/image-alpine)
[![](https://badge.imagelayers.io/scaleway/alpine:latest.svg)](https://imagelayers.io/?images=scaleway/alpine:latest 'Get your own badge on imagelayers.io')

Scripts to build the official Alpine image on Scaleway

This image is built using [Image Tools](https://github.com/scaleway/image-tools) and is sourced from the official [Alpine Linux docker repository available on Docker Hub](https://hub.docker.com/_/alpine/).

<img src="http://alpinelinux.org/alpinelinux-logo.svg" width="400px" />

---

**This image is meant to be used on a VC1, START, or C2 server.**

We use the Docker's building system and convert it at the end to a disk image that will boot on real servers without Docker. Note that the image is still runnable as a Docker container for debug or for inheritance.

[More info](https://github.com/scaleway/image-tools#docker-based-builder)

---

## Install

Build and create your image using [Image Tools](https://github.com/scaleway/image-tools):

    image-tools $ make IMAGE_DIR=/path/to/image-alpine/latest/ EXPORT_DIR=$(mktemp -d) scaleway_image

Full list of commands available at: [scaleway/image-tools](https://github.com/scaleway/image-tools/tree/master#commands)

---

A project by [![Scaleway](https://avatars1.githubusercontent.com/u/5185491?v=3&s=42)](https://www.scaleway.com/)
