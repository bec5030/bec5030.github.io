---
layout: post
title: Chia Cryptocurrency Farming
categories: [Cryptocurrency]
featured-image: /images/chia_farming/chia.jpg
---

A quick post about my Chia farming setup.

Recently, I set up hardware to farm Chia. Chia is an interesting cryptocurrency as it uses what is called “proof of space” for a more green consensus implementation than proof of work. And in this case, it is called “farming” instead of mining. It uses hard drive storage in roughly 100-110 GB increments to farm, consuming limited power. I will consider this investment a great success if I can get enough return to pay off the hard drives and effectively get them for free.

The 100-110GB increments are called plots. The creation of all the plots is an entirely consuming task in itself, which took many days to complete even with fast NVME SSDs. More than anything, though, it was weird to me to be working with such large datasets. Transferring 100GB isn’t something you can just quickly upload to the cloud or stick on a flash drive to move to a different location.

I decided to get three different types of drives for this setup: two super cheap, low-quality, internal 4 TB drives; two super portable 5 TB drives, which run off USB power; and 2 huge, externally powered 14 TB drives. In all, it consumes 44.4 terabytes of plots to be farmed.

The cool part of this setup is a Raspberry Pi is the host for all the drives. An adapter was purchased to give a USB interface to the internal drives, and a powered USB expander was purchased to handle the extra power needs that the Raspberry Pi cannot deliver. I wrote scripts to automatically mount the drives on boot and start the farming application. This system can be restarted remotely from a smart outlet, and if it proves necessary, I will add fault detection logic to handle reliability issues. So far, this has been unnecessary. It's a fun little setup with about a 3-year return on roughly $1,000 in hard drives.

![an image alt text]({{ site.baseurl }}/images/chia_farming/chia.jpg "The Chia setup")
The Chia setup.
