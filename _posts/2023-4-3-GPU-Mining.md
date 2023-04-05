---
layout: post
title: Cryptocurrency GPU Mining
---

A quick post about my GPU mining setup.

I started my professional engineering career creating a hardware bitcoin wallet. As such, cryptocurrency is something I have found interesting over the years. In 2017 I took the step to get into the mining scene, starting with GPUs and eventually transitioning to FPGAs. With the GPUs my goal was to have a very quiet, cost effective system. I landed on Nvidia GTX 1060 and AMD RTX 480/580 GPUs which prove to be an excellent choice.

I maxed out two motherboard PCIe slots, 11 GPUs in all, all my mining Ethereum. I installed a power monitoring system to track power use, a dedicated breaker to handle the power requirements, and set up software to allow remote control of the systems. The setup required using GPU risers that gave PCIe x1 connections to each graphics card. Additionally, I had to chain multiple PSUs together to provide enough power and power ports. The systems were without a case, providing the required space to fit all the GPUs, as well as provided the benefit of easy access to all the components in the system. The GPUs sat on a custom metal fixture that I built to hold them. Images of the setup can be seen below.

![an image alt text]({{ site.baseurl }}/images/gpu_mining/gpu_rig1.jpg "The first GPU rig")
The first system with 4 Nvidia GTX 1060s, and 2 AMD RX 580s.
![an image alt text]({{ site.baseurl }}/images/gpu_mining/gpu_rig2.jpg "The second GPU rig")
The second system with 4 AMD RX 580s, 1 AMD RX 480, and two power supplies coupled together.


The graphics cards were each individually tuned, and optimized for the power efficiency per hashrate. The GTX 1060s provided easy runtime tools for tuning, while the RX 580s required modding and replacing the graphics card bios with different memory timings and installing the right drivers for compute mode. The hardest part however was getting the motherboards to recognize all the graphics cards simultaneously. A very slow delicate process of trying to find the right order/PCIe slot combo to recognize each additional card one at a time. Ultimately, I was able to run these cars for several years, recuperating the cost of the hardware and providing a nice space heater in the winter. 

Pictured below are the two motherboard setups hosting the 11 GPUs.

The GPUs have since found their way to new homes.

![an image alt text]({{ site.baseurl }}/images/gpu_mining/gpu_rig_both.jpg "Whole view of setup with both GPU rigs on display")
The full setup with all of the GPUs.
