---
layout: project
title: Audio Mixer
description: Hardware and software development project on Zynq-7000 ZedBoard
published: false
---

This is a final project for IAS0550 Systems-on-Chip class which combines hardware (HW) design on FPGA and embedded software (SW) development.
Both HW and SW was developed for [Zynq-7000 ARM/FPGA SoC Development Board](https://www.avnet.com/wps/portal/us/products/avnet-boards/avnet-board-families/zedboard/){:target="_blank"}. In this project, I gained an extensive understanding of how HW is interfaced with SW, learned to customize provided HW IP to specific needs, and got hands-on experience in embedded Linux development by writing drivers in C.

<a href="" target="_blank"><span class="label">View source code</span></a>

## Project task

Audio Mixer is a processing system that takes in 2 audio data streams and mixes them into a single stream. Before being mixed, the audio streams pass
through IIR filters (which are set-up to work as equalizers) and gainers (increase/decrease the volume). The task was to develop such system satisfying the following conditions:

1. First audio stream must be received from network via Linux driver
2. Second audio stream must be received from Line In audio input of the board
3. The volume and equalizers of both audio streams must be controlled separately
4. System must be controllable through UI (CLI, OLED display and switches/buttons)

{:refdef: style="text-align: center;"}
![system design]({{ '/assets/images/soc/soc_design.png' | prepend: site.baseurl | prepend: site.url }} "Visual representation of the system")
{: refdef}

## Solutions

Some IP and drivers were already provided, thus below are only solutions that were implemented entirely by me and my teammate. Modules of the system operate in parallel with help of threading.

### Audio reception from network

Audio stream from network was received as packets of 1024 bytes consisting of 512 audio samples. In order to keep the flow synchronized, a Linux FIFO was used to stack the incoming packets and then play them back. Every single audio sample (of 2 bytes) was then read from the FIFO into HW registers at a rate of 48 kHz (equalizer operatong frequency). Paralellism was achieved using POSIX threads, where network listener was launched as a standalone thread. After samples are written into registers, they had to mapped to AXI bus in order to be interfaced with other IP blocks of the system. Luckily, Vivado provides AXI bus IP and all that had to be done was to sign extend the sample to be 24 bits from original 16 bits.

### Switches control

Switches on ZedBoard are a part of GPIO and I decided to use them for equalizer settings. In order to efficiently monitor and respond to changes in switch states, I had initialized Linux GPIO file descriptors of switches and stored them in an array of ***pollfd*** structure. From there, it was monitored by a Linux-provided function ***poll()***. Every time a change in any of the switches would happen, the signal would be passed to a designated register of an equalizer and a value in OLED display would be updated to reflect the state of equalizers.

{:refdef: style="text-align: center;"}
![OLED with switches on ZedBoard]({{ '/assets/images/soc/oled_board.png' | prepend: site.baseurl | prepend: site.url }} "OLED with switches on ZedBoar")
{: refdef}

### Volume control

To keep things simple, volume is controlled through a CLI. When user chooses to change the volume, he is asked to choose which audio stream volume to increase/decrease and is then asked to enter a value. The values are passed to a designated register of a respective volume gainer.

{:refdef: style="text-align: center;"}
![CLI User Interface for volume control]({{ '/assets/images/soc/soc_UI.png' | prepend: site.baseurl | prepend: site.url }} "CLI User Interface for volume control")
{: refdef}

## Acknowledgments