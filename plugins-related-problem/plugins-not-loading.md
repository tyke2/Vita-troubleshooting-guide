---
description: halp they ate all my ram
---

# Plugins not loading

Dealing with plugins is kind of annoying and hard to debug in some cases. If it bootloops, we need to find the culprit plugin(s) through a witch hunt. Fortunately, through previous community experience, we can narrow down the issues.
  


## Plugins are programs.

It may sound unrealistic, but plugins are small programs that can affect the system noticeably. The more plugins you try to load, the more system resources they will need, like RAM. If it asks for too much, it will lead to a bootloop. This is why you should only install essential and useful plugins, so you don't end up ruining your Vita's performance.  \(Someone once reached me because he couldn't boot his vita after installing ALL the plugins he found in autoplugin 2\)  
  
We will take an example a common case I could find during a time when I acted as a helper :   
  


```text
# This file is used as an alternative if ux0:tai/config.txt is not found.
# For users plugins, you must refresh taiHEN from HENkaku Settings for
# changes to take place.
# For kernel plugins, you must reboot for changes to take place.
*KERNEL
ur0:tai/minivitatv.skprx
ur0:tai/ds3.skprx
ur0:tai/music_premium.skprx
ur0:tai/PSVshell.skprx
ur0:tai/storagemgr.skprx
ur0:tai/plugins/vitabright.skprx
ux0:app/PSPEMUCFW/sce_module/adrenaline_kernel.skprx
ur0:tai/plugins/nonpdrm.skprx
ur0:tai/ioplus.skprx
ur0:tai/AnalogsEnhancer.skprx
ur0:tai/NoPowerLimits.skprx
ur0:tai/0syscall6.skprx
ur0:tai/ds4vita.skprx
ur0:tai/udcd_uvc.skprx
# henkaku.skprx is hard-coded to load and is not listed here
# main is a special titleid for SceShell
ur0:tai/henkaku.suprx
*NPXS10015
# this is for modifying the version string
ur0:tai/henkaku.suprx
*NPXS10016
# this is for modifying the version string in settings widget
ur0:tai/henkaku.suprx
*main
ur0:tai/LowMemMode.suprx
ur0:tai/plugins/download_enabler.suprx
ur0:tai/plugins/shellbat.suprx
ur0:tai/volume_profile.suprx
ur0:tai/quick_volume.suprx
*ALL
ur0:tai/BackTouch2L2R2.suprx
ur0:tai/vitagrafix.suprx
ur0:tai/remaPSV.suprx
*NPXS10013
ur0:tai/ps4linkcontrols.suprx
```

OwO  
That's a lot of plugins! No wonder his vita doesn't load anymore. Unfortunately in most bootloop cases, the config looks like this. So let's take this exemple and see how we solve it.
  
\*not talking about the fact that he put some plugins inside a plugins folder which is not recommended\*  


## Installing multiple plugins that do the same thing

Yep, that's his first mistake. Let's take a closer look.  
The guy wants to use his DS4 plugins, but he loaded all the plugins for it : minitv, ds3 and ds4.  
He needs to make a choice, either use minitv or ds4. In this case let's go with minitv \(which uses DS3 as a dependency\)  


## SD2VITA and ioplus plugin not being at the top.

Another common mistake is to not put the sd2vita at the begining of \*KERNEL. This is very important as normally every plugins need to be loaded after the storage is mounted or else there will be problems upon boot because of the sudden storage change.  
As for ioplus, it is a dependency used by other plugins to have access to more IO operations in userland. It need to be loaded before them.

## Loading heavy plugins when we don't always use them

The Ucdcd uvc plugin for streaming the psvita screen through usb is one of the most heavy plugins, so it needs a lot of resources. If you want to use it, make some room for it. Let's see :

* I don't think you need to activate the music related plugins, that already removes 3 plugins from the list. 
* PS4 link controls? Not useful in that case. 
* Nopowerlimit, unless you really want to let the wifi open when playing a demanding game, can be removed.
* The Adrenaline plugin is one of the most useless plugins there, since all it does is allow you to not launch Adrenaline twice. \(one time to inject the adrenaline.skprx, and a second time to open adrenaline\). Let's free our config from this one too.
* Using remap plugins, analog enhancer and BackTouch when we use a DS4 controller is also useless. It's just wasting memory at this point since you will use your PS4 controller and not the vita controls. We did some cleanup so let's see how the config looks like. 

```text
# This file is used as an alternative if ux0:tai/config.txt is not found.
# For users plugins, you must refresh taiHEN from HENkaku Settings for
# changes to take place.
# For kernel plugins, you must reboot for changes to take place.
*KERNEL
ur0:tai/storagemgr.skprx
ur0:tai/minivitatv.skprx
ur0:tai/ds3.skprx
ur0:tai/ioplus.skprx
ur0:tai/PSVshell.skprx
ur0:tai/vitabright.skprx
ur0:tai/nonpdrm.skprx
ur0:tai/0syscall6.skprx
ur0:tai/udcd_uvc.skprx
# henkaku.skprx is hard-coded to load and is not listed here
# main is a special titleid for SceShell
ur0:tai/henkaku.suprx
*NPXS10015
# this is for modifying the version string
ur0:tai/henkaku.suprx
*NPXS10016
# this is for modifying the version string in settings widget
ur0:tai/henkaku.suprx
*main
ur0:tai/LowMemMode.suprx
ur0:tai/download_enabler.suprx
ur0:tai/shellbat.suprx
*ALL
ur0:tai/vitagrafix.suprx
```



It looks way more clean now. As you have seen, people always tend to load more plugins than they really need. Using plugins you only need for the game session you will do allows you to enjoy your system without being blocked by bootloop. You can create multiple config.txt for each case if you want as long as the config isn't heavy \(more than 10 plugins at the same time is not recommended\).  
By following the same logic you can clear your config.txt easly without scratching your head over why it won't boot.   
  
  




