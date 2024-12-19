+++
title = "Asustor Flashtor 6 with TrueNAS Scale"
description = "Unclouded - host your own cloud"
date = 2024-12-17

[taxonomies]
tags = ["NAS", "TrueNAS", "Asustor"]

[extra]
copy_button = true
+++

# Motivation: Away from the cloud

We all appreciate the convenience of cloud storage, it's just always (well almost always) available. Your photos, videos, documents, whatnot are just up there, in the cloud, with highly available storage, highly available network, highly available compute. But that's the thing though: cloud is just someone else's computer as we all know.

What if is there is a [global IT outage](https://www.weforum.org/stories/2024/07/global-outage-it-cyber-resilience-alarm-world/) and you need to access your documents at that exact moment? Let's say you saved your booking confirmation and you are about to check in, but the service is down. 

Or what if your (cat)photos get leaked by the cloud provider? Did I mention the ever increasing cloud subscription prices?

# Host your own "cloud"

Enter: the [Asustor Flashtor 6](https://www.asustor.com/en/product?p_id=79). It's a NAS with a 6-bay NVMe SSD capacity and dual 2.5Gbps network ports. Although it comes with only 4GB of RAM, you can actually swap out the modules and upgrade to up to 32GB. So that's exactly what I did:
```
admin@truenas:~$ free -m
               total        used        free      shared  buff/cache   available
Mem:           31864        9446       22151         203         919       22418
Swap:              0           0           0
```

The factory default [ADM (Asustor Disk Manager) firmware](https://www.asustor.com/service/release_notes) is kind of okay at first, but as I started to setup things I needed and the way I liked them, I realized it's not the best fit for my use case.

So after considering the options, I installed the latest [TrueNAS Scale](https://www.truenas.com/truenas-scale/) on it. The internal storage is too small for TrueNAS scale, and to save all the 6 NVMe bays for data storage, I've got a [480GB external USB 3.1 SSD](http://www.kingmax.com.tw/en-global/product/product/Model/Portable_SSD_KE31) that I use for the OS.

For data storage, I've got [4x 2TB NVMe SSDs](https://www.westerndigital.com/en-us/products/internal-drives/wd-black-sn850x-nvme-ssd?sku=WDS200T2X0E-00BCA0):
```
root@truenas[~]# nvme list
Node                  Generic               SN                   Model                                    Namespace Usage                      Format           FW Rev  
--------------------- --------------------- -------------------- ---------------------------------------- --------- -------------------------- ---------------- --------
/dev/nvme3n1          /dev/ng3n1            XXXXXXXXXXXX         WD_BLACK SN850X 2000GB                   1           2.00  TB /   2.00  TB    512   B +  0 B   620361WD
/dev/nvme2n1          /dev/ng2n1            XXXXXXXXXXXX         WD_BLACK SN850X 2000GB                   1           2.00  TB /   2.00  TB    512   B +  0 B   620361WD
/dev/nvme1n1          /dev/ng1n1            XXXXXXXXXXXX         WD_BLACK SN850X 2000GB                   1           2.00  TB /   2.00  TB    512   B +  0 B   620361WD
/dev/nvme0n1          /dev/ng0n1            XXXXXXXXXXXX         WD_BLACK SN850X 2000GB                   1           2.00  TB /   2.00  TB    512   B +  0 B   620361WD
```
That leaves me 2x NVMe bays for future expansion.

My datasets are [encrypted ZFS datasets](https://www.truenas.com/docs/scale/scaletutorials/datasets/encryptionscale/), in case someone were to physically access the NAS.

# Apps, apps, apps

TrueNAS Scale has a containerized approach to runnings apps. Honestly, the initial setup of the apps was a frustrating PITA experience, due to being in a [transition period from k3s to Docker](https://forums.truenas.com/t/removal-of-k3s-based-apps-from-truenas/6467) at the time doing this setup.

But after some ~FAFO~ experimenting, I've got my apps running:
- [Tailscale](https://tailscale.com/) : VPN, so that I can access my stuff on the NAS from anywhere. Note: enable host-network for the Tailscale container, and add `--advertise-routes=x.x.x.x/24` (replace it with your home network CIDR) as an extra argument to access your other apps remotely.
- [Nextcloud](https://nextcloud.com/) : to store and sync my photos, videos, documents
- [Prowlarr](https://prowlarr.com/), [Radarr](https://radarr.video/), [Sonarr](https://sonarr.tv/), [Lidarr](https://lidarr.audio/), [Transmission](https://transmissionbt.com/) : to download, seed, organize my Ubuntu ISO files, Ubuntu ebooks and Ubuntu related TV shows / movies
- [Plex](https://www.plex.tv/) : to watch my Ubuntu related movies and TV shows

Yeah, I get it, one could just actually run baremetal Ubuntu/Debian/Arch/whatever and setup everything manually. But I was looking for a way to keep future maintenance as minimal as possible, so I'm happy with the current setup after the initial learning curve.

# Conclusion

I'm able to sync my files&photos from my laptop, iPhone, iPad (having them all running Tailscale) with the NextCloud app. Plex also works, as long as I have decent internet connection. Basically it's a "setup and forget about it" kind of arrangement, which is exactly what I want.