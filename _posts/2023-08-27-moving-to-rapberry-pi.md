---
layout: single
title: Moving to Raspberry Pi 
permalink: "/posts/moving-to-rapberry-pi/"
date: "2023-08-27"
future: true
toc: false
published: true 
excerpt: "I have been moving most of my stuff to Raspberry Pi. This blog was pending and it is now moved as well. Why, you ask?"
header:
  overlay_image: /assets/images/posts/moving-to-raspberry-pi/raspberry-pi-on-refrigerator.jpg
  overlay_filter: rgba(0, 0, 0, 0.4)
tags:
  - vaibhav
  - devops 
  - backend
---

Recently I discovered the way using which I could just host my websites right from my home and since then to save some money (but honestly more because I love tinkering for setups) I thought why not move most of the stuff to the Raspberry Pi that I already have. You can see the one I have sitting on top of my refrigerator. It was already being used within the network for storing files, as well as a DNS server with help from [PiHole](https://pi-hole.net/). So I started with opening ports for PiHole admin and so on. Recently I also found how to serve a static HTML site using Nginx over internet from my Pi. Since this blog was already a static site made with Minimal Mistakes Jekyll theme, I thought why not use the opportunity to move this site from the cloud to the Raspberry Pi as well!

In addition, since this blog is to serve as a shared blog among the members of the [Techrail GitHub Org](https://github.com/techrail), I thought I could just setup a git workflow with a cron job to make periodic updates (much the same way GitHub pages behaves). I think the git script is ready but we still need to test if the cron works. 

Test 1