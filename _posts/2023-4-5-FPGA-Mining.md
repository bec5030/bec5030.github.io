---
layout: post
title: Cryptocurrency FPGA mining systems, plus my adventures in water cooling!
categories: [Cryptocurrency, FPGA]
---

A post about my FPGA mining setup.

### Introduction
My cryptocurrency mining aspirations grew from GPUs to FPGAs as I gained more hands-on FPGA experience from class and my master’s thesis research. FPGAs appear to be the perfect solution for cryptocurrency mining as they provide the highest flexibility and efficiency combination. In reality, they suffer from a high cost of hardware, difficult resale, slow development time (which makes board support even harder), extreme optimizations to be competitive, a small development community, and a fractured hardware ecosystem. Additionally, FPGA cooling and power delivery are difficult obstacles when trying to maximize chip use. Had I not known how to develop for FPGAs myself, and thus been at the mercy of others, I never would have jumped in. But I knew how, and with that as my fallback, I made a huge investment and bought two SQRL BCU1525 boards. BCU1525s are Xilinx Virtex Ultrascale+ VU13P boards with a PCIe interface. I also bought a few SQRL Acorn CLE-215+ boards. These are M.2 PCIe x4 interfaced Artix-7 FPGAs. A few years later, I also added a SQRL Forest Kitten 33 (FK33), a PCIe interfaced Virtex Ultrascale+ VU33P board with high bandwidth memory (HBM2). The design of the BCU1525 lent itself to compute heavy algorithms, the tiny Acorns designed for GPU compute offloading and assist (my personal favorite), and the FK33 for memory bandwidth and memory latency intensive algorithms.

{:refdef: style="text-align: center;"}
![an image alt text]({{ site.baseurl }}/images/gpu_mining/gpu_rig1.jpg "The initial setup with GPUs."){: width="350" }
{:refdef}


The initial setup with GPUs.
{:refdef}

### BCU1525
The BCU1525, the most significant of the three, is equal to roughly 10 Acorns and 4 FK33s. It is a beast of an FPGA with over 2 million LUTs. For this BCU1525 system setup, I built a mid-range Zen2 computer and hooked the BCU1525 boards up via PCIe. From there I was off to the races! Or so I thought… The boards came with a heatsink, but I opted to purchase the upgraded heatsink and fan for even better cooling. The fan was a centrifugal or radial fan that appeared to work somewhat, but the cards could not be pushed to their limits with confidence. More significantly, the fans were loud. Very loud. Keeping this setup in my room was not an option, and moreover, neither was putting it in the attic! Something needed to be done, so I reluctantly went down the rabbit hole of water cooling.

![an image alt text]({{ site.baseurl }}/images/fpga_mining/bcu1525_extended_heatsink_1.jpg "The BCU1525 with extended heatsink."){: width="350" }
{:refdef}

The BCU1525 with extended heatsink.
{:refdef}

![an image alt text]({{ site.baseurl }}/images/fpga_mining/bcu1525_extended_heatsink_2.jpg "The initial setup with both BCU1525s and extended heatsinks."){: width="350" }
{:refdef}

The initial setup with both BCU1525s and extended heatsinks.
{:refdef}


Water cooling sounds cool and seems easy enough, but it turned out to need a lot of research, be very costly, and be incredibly annoying to maintain. The setup is, however, super quiet and great at cooling. The biggest thing I was concerned with was mixing metals. Mixing two different metals will cause them to corrode and destroy the system. The parts of the system include the heatsink and back plate for the FPGA boards, radiators and fans to remove heat, tubing to provide a path for the water, fittings to connect all the tubing, pump to move the water through the system, coolant, reservoir to hold coolant, a port expander to plug in all the fans. I additionally added extra heatsinks and fans to the backplates of the FPGAs to help further  remove heat from that side of the board. The radiators and pump (d5) were spec-ed to meet the thermal dissipation needs of at least 2x350 watts. Fitting all the radiators, tubes, pump, and reservoir was more of a challenge than anticipated, but worked out in the end. In all, I believe it came out to about 2x$200 for the heatsinks and roughly $600 for the rest. Although the coolness factor is pretty high, the cons of the system make me wish I didn't have to go this route. Changing the coolant every 4 to 6 months is exceptionally annoying. Even with this effective cooling solution and high quality EVGA power supply, the power port fried on both cards and needed replacement, which was a difficult task during the height of Covid. My boards were knocked offline for several months.

![an image alt text]({{ site.baseurl }}/images/fpga_mining/bcu1525_waterblocks.jpg "The boards with and without the waterblock."){: width="350" }
{:refdef}

The boards with and without the waterblock.
{:refdef}

![an image alt text]({{ site.baseurl }}/images/fpga_mining/bcu1525_watercooling.jpg "The watercooling system."){: width="450" }
{:refdef}

The watercooling system.
{:refdef}

### FK33
The FK33 has a much lower power dissipation requirement and can adequately be cooled off with a heatsink and axial fan combo. The axial fan is very quiet and requires no modification. Thus far, the full PCIe bandwidth has not been necessary. In fact the PCIe interface has not been used for communication at all. As such the FK33 has been installed in a PCIe riser for power delivery, and only a USB cable has been required for communication. This means with the right host firmware, a raspberry pi or other single board computer can be used. The FK33 has huge amounts of memory in comparison to its logic availability, really lending itself to applications that require the awesome bandwidth and latency of the high bandwidth memory interface. So far it has mostly been used to mine Ethereum very efficiently, much more efficiently than a GPU from the same generation.

### Acorn
The Acorn is the most interesting and awesome board to me. It is the lowest cost by a large margin which eliminates the scary price barrier of entry. But more than anything, I really love the idea of heterogeneous computing, which is why I joined the Heterogeneous Computing Research Group at RIT for my master’s. Heterogeneous computing is the concept of having different types of computer processing within the same system, and tailoring applications or parts of applications to different hardware to have more effective computation.

The concept was to pair an Acorn with GPUs and offload computation heavy, or GPU inefficient parts of algorithms to the Acorn, such as the Keccak steps in the Ethereum hashing algorithm. The challenge with this is the amount of data that needs to be passed back and forth, which is why the Acorn was given an M.2 PCIe x4 interface capable of pushing a lot of data for the relatively tiny FPGA. Unfortunately, this idea never came to fruition. I would have loved to implement it myself but never got around to it while the value was there. GPU advancements, algorithm implementation optimizations, and coins moving to entirely new algorithms made this not a worthwhile implementation eventually.

However,  I did use the Acorns to create a personally developed mining program. This program  used only Acorns, no other hardware for the algorithm offloading. This is a feat I am very proud of. Utilizing the Acorns for cryptocurrency purposes is something no one else has done in the mining community! More about this will be discussed in an upcoming post!

Since the value of Acorns never materialized, they can now be bought second hand for a great price. I believe they have incredible value for use in Software Defined Radio (SDR) applications. There is also potential value for them in other applications, such as video game emulation, but I feel less strongly about this.

![an image alt text]({{ site.baseurl }}/images/fpga_mining/acorn.jpg "The mighty Acorn."){: width="350" }
{:refdef}

The mighty Acorn.
{:refdef}

### Acorn limits

I learned a lot about the limitations of the Acorn while developing for it. The board fits into an M.2 slot but has an adorable little heatsink and fan. The heatsink is very tall for the part so it needs a lot of clearance. It will never fit into a laptop as is. The worst part, however, is the annoying high-pitched squeal of the fan. 

There are three critical flaws with the board, all having to do with the power chip on the board. The first issue, which is not the limiting factor, is that the power chip is unable to provide the maximum power the FPGA can handle. Without looking into it, I suspect the part was chosen to meet the maximum power that can be delivered in the M.2 spec. An unfortunate limitation. 

The second issue is the actual limiting factor currently, which is heat dissipation of the power chip. Unfortunately the heatsink does not extend far enough to touch the power chip. A small heatsink can be added which also gets air blown over it from the fan, greatly improving performance capacity, but still, it is inadequate. Three approaches have been considered but have not been tested yet. These approaches are to use a centrifugal fan, use a Peltier cooler, and create a mini water cooling solution. 

The last issue is a board routing issue that leaves a temperature monitoring ADC pin with a floating reference. The pin has enough exposure to remedy the problem if you are so determined.  I figured out a way to solder to a PCIe riser ground and get accurate readings without having to modify the Acorn itself. I tried using a thermal camera to correlate the floating values with the temperature, but that was not very successful. Without an accurate reading, it makes an already limiting factor even more restrictive.

![an image alt text]({{ site.baseurl }}/images/fpga_mining/acorn_power_heatsink.jpg "The mighty Acorn with tiny heatsink on power chip."){: width="350" }
{:refdef}

The mighty Acorn with a tiny heatsink on the power chip.
{:refdef}

### Extra thoughts
I believe that the advantages of FPGAs can be greatly increased if dual or multi-mining is implemented. Often, many algorithms lend themselves best to specific parts of an FPGA, such as LUTs, DSPs, or BRAMs/URAMs, leaving the other parts unutilized. By selecting a combination of algorithms, the FPGA can be further taken advantage of, providing a higher value proposition. Unfortunately, this has not come to fruition yet, but I believe it holds great potential.



