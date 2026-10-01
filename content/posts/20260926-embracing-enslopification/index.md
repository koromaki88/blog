---
title: "Using NixOS to slop more securely"
date: 2026-09-26T20:15:00+07:00
draft: true
tags: ["AI", "Linux", "NixOS", "Hardening", "Virtualization", "QEMU"]
categories: ["Writeups"]
summary: "Attempting to integrate AI agents into work and somehow ended up trying out NixOS."
cover:
    image: "cover.png"
---
yes I drew the cover. call it human slop

---

# Preface
Finally addressing the giant elephant in the room - artificial intelligence. 

For the past year, I have been experimenting with AI agents in my workflow & study. Suffice to say, it does everything better than I do, and sometimes I become over-reliant on it that I have to pay the price. But that is a story for another day.

One thing became very obvious early on when I begin using the tool: security and privacy. It really surprises me when I realize the majority of developers and avid users do not seem to mind giving AI access to your tools and files so easily. At its core, the agent is a complete black-box, non-deterministic machine handed to you by a proprietary third-party provider. Open source harnesses exists to better control their functionality, but fundamentally the actual model is something the majority of us would never understand the inner workings of. [Even the companies themselves cannot keep their magic tool under control](https://en.wikipedia.org/wiki/OpenAI%E2%80%93HuggingFace_incident).

Fortunately, I am a paranoid person. The last thing I want is for an AI to accidentally wipe out my entire computer and its only response to me is "*Oopsie daisy, I messed up!~ You have to figure out how to fix this now...*" This post documents some measures I have taken to securely isolate the agent, while still providing necessary convenience yet maintaining sufficient caution.

# Virtual Machine
The current standard for safely isolating software is using virtual machines. I use QEMU on my machine since they are lighter and have better compatibility with my linux host machines. I have previously written [a post on how to set it up](../20250605-qemu-guide-arch/) specifically for Arch Linux, though it should still work for most distributions. For alternatives:
- VirtualBox works fine, but from my experience they are slower and consumes more resources - this is especially important since I wanted to keep it lightweight.
- VMware - I do not have an opinion on since I have not tried it.

By default, a Linux VM generally has sufficient isolation. NAT network is a possible attack vector, but most of my tasks involving AI agents rarely involve directly interacting with the host or local network.

# Operating System
For the guest OS, I picked NixOS. Previously, I have experimented with Arch/Debian, but there are two caveats:
