---
layout: post
title: My Windows 10 installation checklist
category: Computer Science & Technology
tags: ["technology", "guide"]
date: 2026-10-02 17:32 +0100
---
First, some waffle.  

On the surface, automobiles are not similar to our personal computers[^1]. The car's purpose is usually[^2] to transport people across land, while the computer's purpose is generally to *compute* - computing everything from video rendering to.... audio rendering?  

If you're American, then Henry Ford invented the car[^3]. At that point in time, the business strategy was probably something like "Let's invent new ways to make our product more affordable while still maintaining a profit".  

Today, this idea has been pushed to its absolute limit - so much so that we now don't own many of the *products* that we use - sorry, I meant *services*.  
Now, everything is about producing a product as cheaply as possible, then actually selling it to you when you have it in your hands, usually in a subscription model. Look no further than [BMW's heated seats subscription](https://www.bbc.co.uk/news/technology-62142208)!  
Better yet, why should the company be trying to sell you something, when they could just sell *you?* Auto manufacturers love doing this[^4] - along with every other technology sector, of course. They will sell *everything* they can about you.  

Computers, specifically operating systems and software have tread a very similar path. Ads baked into the OS, which said OS then promply measures your response to that ad, to show you more ads.  

The point I'm trying to make is that you should **maintain your computer like you would a car** - especially now that they're so central to our digital lives.


[^1]: I mean, essentially all cars have some sort of computer inside them.  
[^2]: At first I was going to say auto racing - but think about it hard enough, you'll realise most forms of motorsport racing are just "*who can traverse this track the fastest?*"  
[^3]:  A depressing amount of people believe this.  
[^4]: Here's an [informative video](https://www.youtube.com/watch?v=J7oTWytFCmE).

---

## The checklist

The checkboxes are clickable, however they are not persistant so they will disappear upon a browser refresh.  
> I am not an expert, nor am I a typical Windows power user. Everything here is my way of doing things. 
{: .prompt-info }  

---

## Pre-installation/Wiping

This section is dedicated to everything before installing Windows 10. Ignore if you have already wiped and installed.  
> I am, of course, not responsible for any damages or data loss. Don't blindly follow any tutorials or guides - make sure you understand what you're doing!
{: .prompt-danger }  

<label><input type="checkbox"> Ensure all important data is backed up</label>  

<label><input type="checkbox"> Write information on target drives</label>  
If your system has multiple drives and you're only wiping one, write down the drive information - so you don't format the wrong drive!  

<label><input type="checkbox"> Obtain installation media ISO</label>  
If you don't have a valid Windows 10 ISO, you can create an ISO using Microsoft's [Media Creation Tool](https://www.microsoft.com/en-gb/software-download/windows10).  

<label><input type="checkbox"> Flash installation media to USB before wipe</label>  
Remember to do this before you wipe your PC, otherwise you won't have a PC to flash the USB!  
Tools like [Rufus](https://rufus.ie/en/) can flash the ISO to your USB drive. Rufus in particular has options for skipping annoying parts of Windows setup, such as auto opt-out of Windows telemetry services.  

<label><input type="checkbox"> Download and flash [ShredOS](https://github.com/PartialVolume/shredos.x86_64) to USB</label>  
This is completely optional, of course. You can format and delete the old data in the Windows installation menu. I just really enjoy the peace of mind that the old data is securely gone, not hanging around anywhere for a fresh start.  
If you only have one USB available, [Ventoy](https://www.ventoy.net/en/index.html) allows multiple ISOs to boot from one USB. I highly recommend!  

<label><input type="checkbox"> Disable Secure Boot and any SSD protection settings in BIOS</label>  
These often interfere with ShredOS and Ventoy.


<label><input type="checkbox"> Wipe target drive(s)</label>  

> Do not use the nwipe GUI for wiping SSDs, nVME or SATA! 
{: .prompt-warning }  

Depending on what kind of drive you have, follow the appropriate steps.

#### For HDDs
Target your drives and choose an erase method using the nwipe GUI. Hit erase, and you're done.

#### for SATA SSDs
The process for SATA SSDs is more complicated. I follow [this guide](https://grok.lsu.edu/article.aspx?articleid=16716) (which I have copied here):

First press `alt-f2` to enter the terminal in ShredOS.

1. Run `fdisk -l` to find the target disk.
2. Run `hdparm -I /dev/sda` - this will tell you if the disk is frozen.  
It should also tell you the estimated completion time here.  
3. If the disk is frozen, run `echo -n mem > /sys/power/state` - this will sleep the computer.
4. Wake the computer up, run `hdparm -I /dev/sda` and check if the disk is not frozen.
5. Set a temporary password for the drive - in this case "p". `hdparm --user-master u --security-set-pass p /dev/sda`
> Never leave the password blank! You may risk "bricking" your drive.
{: .prompt-danger }  
6. Once again, run `hdparm -I /dev/sda` and check that security is "enabled". If it says "not enabled", do not proceed.
7.  If the previous command mentions `ENANCED SECURITY ERASE` this means that the drive supports... enchanced security erase. **Ensure you use the same password** (in this case, p).
    - If it does: `hdparm --user-master u --security-erase-enhanced p /dev/sda`
    - If it doesn't: `hdparm --user-master u --security-erase p /dev/sda`

Whew!

#### For nVME SSDs

Much simpler. Run the following:
```bash
nvme list
nvme format /dev/nvmeXnY -s1
```
Where X and Y is the target drive.

## During installation

<label><input type="checkbox"> Do not connect to internet during setup</label>  
Don't do this - Microsoft will force a microsoft account and the Office suite down your throat.  
<label><input type="checkbox"> Do not create a Microsoft account if possible</label>  
They make this quite hard in Windows 11, but it is possible in Windows 10, dependant on what version you are using.  

## First steps after installation

<label><input type="checkbox"> Connect to the internet</label>  
<label><input type="checkbox"> Install [Chrome](https://www.google.com/intl/en_uk/chrome/), [Firefox](https://www.firefox.com/en-GB/), [Vivaldi](https://vivaldi.com/), [Brave](https://brave.com/), [Opera](https://www.opera.com/) / [Opera GX](https://www.opera.com/gx)</label>  
<label><input type="checkbox"> Install OEM drivers</label>  
This, of course depends on your OEM. But here's a link to [Lenovo System Update](https://support.lenovo.com/ca/en/downloads/ds012808-lenovo-system-update-for-windows-10-7-32-bit-64-bit-desktop-notebook-workstation).  
<label><input type="checkbox"> Install Graphics Drivers - [nVidia](https://www.nvidia.com/en-us/drivers/), [AMD](https://www.amd.com/en/support/download/drivers.html)</label>  
<label><input type="checkbox">  Re-enable Secure Boot in BIOS/UEFI</label>  


## Next steps  

<label><input type="checkbox">  If needed, [MAS](https://massgrave.dev/)</label>  
<label><input type="checkbox">  Check all displays are running at nominal resolution and refresh rate</label>  
<label><input type="checkbox">  Setup Windows Hello fingerprint / face scan</label>  
Obviously, only if you want to, and only if your computer supports it too. Here's a little known fact: On some laptops, if you set a BIOS fingerprint password, the TPM module is on and you have Windows Hello enabled, when booting up the laptop if the BIOS fingerprint successfully scans then Windows will auto-unlock, meaning you don't need to put in your password/fingerprint for the second time.  

<label><input type="checkbox">  Change what the power button does</label>  
Okay, this is a very subjective change. It makes sense for the power button to bind to shutdown. But - if you have a laptop, I highly recommend you set it to **Hibernate** for a few reasons.  
When you close the lid, the computer will go into sleep mode, of course. Sleep mode is a low power mode which keeps your programs and everything else on. However, this means that the battery will slowly sip away, meaning that when you open it two hours later, most the battery has gone. Shutdown is no good either, because it closes everything you were working on.  
Hibernate sucessfully kills two birds with one stone. Press the power button, and the computer will turn off as fast as sleep mode. Your computer has actually shut down, but all open programs have been saved to storage. This means that when you turn on your computer, you're exactly back to where you were just like sleep mode - except the battery has not drained at all. No more dead laptop in the morning!  
Better yet, set it it so that when you close the laptop lid it *still goes into sleep mode*. This means that if you need to move or close the laptop, you won't unnecessarily have to power cycle the laptop.  Importantly, you should set it so that when the lid is closed, the system should go into hibernation after **15 minutes** or so - but *only* if it's not connected to power. You can set all these settings in control panel.  

<label><input type="checkbox">  Check power plan settings</label>  
<label><input type="checkbox">  Disable Sticky Keys intervention</label>  
<label><input type="checkbox">  Customise the wallpaper and accent colour</label>  
<label><input type="checkbox">  Check defaut apps</label>  
While Chrome and other browsers will set defaults for links, often PDFs and other files will still open in Edge.  
<label><input type="checkbox">  Show hidden files and file extensions in File Explorer</label>  
<label><input type="checkbox">  Uninstall pointless preinstalled bloat apps</label>  
<label><input type="checkbox">  Decide what you are doing with Windows Defender</label>  
Personally, I don't have it disabled. There was a time when Defender was astoundingly bad - but it's a lot harder to get malware then it once was, paired with how Defender has improved to passable standard. However, with Windows 10 being discontinued, this might start to change...   



## Common apps
I'm not getting to the specifics yet - here's a quick-fire round of some common apps that many people use on a day-to day basis. Some of these programs could be installed using [Ninite](https://ninite.com/) - but I have never used it, as I prefer to install them myself.  

<label><input type="checkbox"> [Steam](https://store.steampowered.com/about/)</label>  
<label><input type="checkbox"> Office suite/Microsoft 365</label>  
<label><input type="checkbox"> [VLC](https://www.videolan.org/)</label>  
<label><input type="checkbox"> VPN Service ([Proton VPN](https://protonvpn.com/), [Mullvad VPN](https://mullvad.net/en))</label>  
<label><input type="checkbox"> [Spotify](https://open.spotify.com/download)</label>  
<label><input type="checkbox"> [Discord](https://discord.com/)</label>  
<label><input type="checkbox"> [7-Zip](https://www.7-zip.org/)</label>  
<label><input type="checkbox"> [Whatsapp Web](https://web.whatsapp.com/)</label>  
**Note!** I don't install WhatsApp, since I couldn't get it to work with Windows 10. - rather I just installed it as a web app.  
<label><input type="checkbox"> [Todoist](https://app.todoist.com/app/inbox)</label>  
Once again, I just install it as a web app running in Chrome. There is essentially no difference as both programs are just electron/tauri/etc.  
<label><input type="checkbox"> [Zotero](https://www.zotero.org/download/) academic reference manager</label>  
<label><input type="checkbox"> [Audacity v4](https://www.audacityteam.org/) / [Older Versions](https://www.audacityteam.org/download/older-versions/)</label>  
<label><input type="checkbox"> [Paint.NET](https://paint.net/index.html)</label>  
<label><input type="checkbox"> [Obsidian](https://obsidian.md/) note taker</label>  


## Browser Extensions

Here are some that I use.

<label><input type="checkbox"> [uBlock Origin](https://github.com/gorhill/uBlock) / [uBlock Origin Lite](https://chromewebstore.google.com/detail/ublock-origin-lite/ddkjiahejlhfcafbddmgiahcphecmpfh)</label>  
<label><input type="checkbox"> [Dark Reader](https://darkreader.org/)</label>  
<label><input type="checkbox"> [Tampermonkey](https://www.tampermonkey.net/)</label>  
<label><input type="checkbox"> [Zotero Connector](https://www.zotero.org/download/) (requires Zotero app to be installed)</label>  
<label><input type="checkbox"> [SocialFocus](https://socialfocus.app/) social media addiction management</label>  
<label><input type="checkbox"> [Discontinued; still works] [FastForward](https://chromewebstore.google.com/detail/fastforward/icallnadddjmdinamnolclfjanhfoafe) ad.fly bypass</label>  
<label><input type="checkbox"> [Return Youtube Dislike](https://returnyoutubedislike.com/)</label>  
<label><input type="checkbox"> [SponsorBlock](https://sponsor.ajay.app/) auto-skip YouTube paid promotion segments</label>  
<label><input type="checkbox"> [Indie Wiki Buddy](https://getindie.wiki/) avoids fandom.com wikis</label>  
<label><input type="checkbox"> [ColorZilla](https://chromewebstore.google.com/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp) browser eyedroper tool</label>  
<label><input type="checkbox"> External password manager (if you use one)</label>  
<label><input type="checkbox"> [Consent-O-Matic](https://chromewebstore.google.com/detail/consent-o-matic/mdjildafknihdffpkfmmpnpoiajfjnjd
) auto-fill GDPR consent forms</label>  

## Power user / developer tools  

Tools to satiate the curious and demanding. Of course, since everyone's workflow is different here, I'll only include the most surface level stuff here.

<label><input type="checkbox"> IDE: [Visual Studio Code](https://code.visualstudio.com/), [Jetbrains](https://www.jetbrains.com/)</label>  
<label><input type="checkbox"> [Sublime Text](https://www.sublimetext.com/)</label>  
<label><input type="checkbox"> [Git for Windows](https://git-scm.com/install/windows)</label>  
<label><input type="checkbox"> [python.org](https://www.python.org/)</label>  
<label><input type="checkbox"> [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/)</label>  
<label><input type="checkbox"> [Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)</label>  
<label><input type="checkbox"> [Adoptium Prebuilt OpenJDK Binaries](https://adoptium.net/en-GB)</label>  
<label><input type="checkbox"> [Tailscale](https://tailscale.com/)</label>  
<label><input type="checkbox"> [VC++ Redistributables](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist)</label>  
<label><input type="checkbox"> [.NET](https://dotnet.microsoft.com/en-us/download)</label>  
<label><input type="checkbox"> [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/)</label>  
<label><input type="checkbox"> [RubyInstaller](https://rubyinstaller.org/) for Windows</label>  
<label><input type="checkbox"> [LocalSend](https://localsend.org/)</label>  
<label><input type="checkbox"> [Docker Desktop](https://www.docker.com/products/docker-desktop/)</label>  
<label><input type="checkbox"> [Chocolatey](https://chocolatey.org/)</label>  

<label><input type="checkbox"> [Winaero Tweaker](https://winaero.com/winaero-tweaker/)</label>  

## Winaero Tweaker

Winareo Tweaker is a program that allows you to "tweak" settings that Microsoft won't let you. There are hundreds of settings, and while it's tempting to turn all them on, this will result in a massively bloated experience. Don't turn a tweak on because you think it *might* be useful in the future - instead, think about how often you use it, or how useful it is to you right now.  

Here are some (but not all) tweaks that I find useful. 
#### Appearance
<label><input type="checkbox"> Customise startup sound</label>  
<label><input type="checkbox"> Scrollbar Width</label>  
<label><input type="checkbox"> Change System Font</label> 

#### Behavior

<label><input type="checkbox"> Disable ads in Windows</label>  
<label><input type="checkbox"> Auto registry backup</label>  
<label><input type="checkbox"> Disable Aero Shake</label>  
<label><input type="checkbox"> Disable "look for an app in the store"</label>  
<label><input type="checkbox"> Disable automatic maintainance</label>  
<label><input type="checkbox"> Disable downloads blocking</label>  
<label><input type="checkbox"> Disable timeline</label>  
<label><input type="checkbox"> Disable OneDrive</label>  
<label><input type="checkbox"> Disable Windows Update</label>  
<label><input type="checkbox"> Enable Emoji Picker for non-US Languages</label>  
<label><input type="checkbox"> Keep Thumbnail Cache</label>  
<label><input type="checkbox"> Menu Show Delay = 0</label>  
<label><input type="checkbox"> Disable New Apps Notification</label>  
<label><input type="checkbox"> Scrollbar Width</label>  
<label><input type="checkbox"> Show BSOD Details</label>  
<label><input type="checkbox"> Enable .msi in Safe Mode</label>

#### Boot and Logon
<label><input type="checkbox"> Disable OOBE</label>  

#### Desktop and Taskbar
<label><input type="checkbox"> Disable Copilot</label>  
<label><input type="checkbox"> Scrollbar Width</label>  
<label><input type="checkbox"> Disable Live Tiles</label>  
<label><input type="checkbox"> Disable web search</label>  
<label><input type="checkbox"> Make taskbar clock show seconds</label>  
<label><input type="checkbox"> Taskbar button flash count = 0 (infinite)</label>  
<label><input type="checkbox"> Wallpaper Quality = 100</label>  

#### Context Menu

> Choose and pick what you use often here.
{: .prompt-tip }  

#### Microsoft Edge

<label><input type="checkbox"> Tick **every** box</label>  

#### Settings and Control Panel

<label><input type="checkbox"> Disable online and video tips in settings</label>  

#### File Explorer

<label><input type="checkbox"> "Do this for all current items" checked by default</label>  
<label><input type="checkbox"> Disable automatic folder type discovery</label>  
<label><input type="checkbox"> Customise This PC Folders > remve the ones you do not need</label>  
<label><input type="checkbox"> Disable Jump Lists</label>  
<label><input type="checkbox"> Disable Search History</label>  
<label><input type="checkbox"> Enable Auto Completion</label>  
<label><input type="checkbox"> Enable Classic Search</label>  
<label><input type="checkbox"> Enable Recycle Bin for removable drives</label>  

> Only change these settings if you know what you are doing.
{: .prompt-warning }  

#### Network
> Nothing outstanding to change here
{: .prompt-info }  
 
#### User Accounts
> Nothing outstanding to change here
{: .prompt-info }  

#### Windows Defender
> If you want to disable Windows Defender, do it here
{: .prompt-tip }  

#### Windows Apps
<label><input type="checkbox"> Disable auto-update Store apps</label>  
<label><input type="checkbox"> Disable Cortana</label>  
<label><input type="checkbox"> Disable Windows Ink</label> 

#### Battery Report
> Nothing outstanding to change here
{: .prompt-info }  

#### Privacy
<label><input type="checkbox"> Disable password reveal button</label>   
<label><input type="checkbox"> Disable Windows Telementry</label>  

#### Shortcuts
> Add the shortcuts you want
{: .prompt-tip }  

And that's it. This is how I would typically set up a new computer that I use. Everything here is subjective, of course!