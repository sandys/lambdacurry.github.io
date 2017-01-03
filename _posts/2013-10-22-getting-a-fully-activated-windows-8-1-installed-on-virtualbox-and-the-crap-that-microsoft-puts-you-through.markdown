---
author: admin
comments: true
date: 2013-10-22 08:11:37+00:00
layout: post
link: http://www.lambdacurry.com/2013/10/getting-a-fully-activated-windows-8-1-installed-on-virtualbox-and-the-crap-that-microsoft-puts-you-through/
slug: getting-a-fully-activated-windows-8-1-installed-on-virtualbox-and-the-crap-that-microsoft-puts-you-through
title: Getting a fully activated Windows 8.1 installed on VirtualBox - and the crap
  that Microsoft puts you through
wordpress_id: 837
---


	
  * Create a new VM on VirtualBox. Make sure you are running atleast VirtualBox 4.2.16

	
  * run _vboxmanage setextradata <name of VM>  VBoxInternal/CPUM/CMPXCHG16B 1_

	
  * _vboxmanage list vms _- get the UUID for the VM that you just created

	
  * _vboxmanage modifyvm <UUID of VM> --hardwareuuid <some random UUID> _- what this step does is create a hardware uuid for your VM. Now, after you activate windows, you can clone this VM and not lose activation. (Dear Microsoft, this is not to screw you, but give myself the power to be destructive to VMs. I am using a VM, so that I dont have to be too careful with it.)

	
  * Download a Windows 8.1 ISO from [http://winsupersite.com/windows-8/windows-81-tip-download-windows-81-iso-windows-8-product-key](http://winsupersite.com/windows-8/windows-81-tip-download-windows-81-iso-windows-8-product-key)

	
  * Make sure your "network card" in VirtualBox is disconnected. This way you can make a local account, instead of being tied to a Live account. This has a lot of problems just in case you are not connected to the internet at a later stage of using your PC.

	
  * Use a "[Windows 8.1 Generic Key](http://winsupersite.com/windows-8/windows-81-tip-download-windows-81-iso-windows-8-product-key)" to install your Windows 8.1 ISO

	
  * Once Windows is installed, you will need to change the key to your key. To do that, Right-Click the Start button and start the Command Prompt (Admin).
Type the following commands:
_slmgr /ipk YOUR-KEY-WITH-DASHES-HERE_
_slmgr /rearm_
reboot you computer and it should be activated.

	
  * To get full screen on VirtualBox, you **need **to use VirtualBox Guest Additions 4.2.16 ISO (not a higher version - there is a bug)

	
  * For heavens sake uninstall "Skype for Windows 8" tile and install proper Skype from [here](http://www.skype.com/en/download-skype/skype-for-computer/).




God - seriously ? These are all the steps I need to follow to install an OS that I have **bought **on VirtualBox ? This is bullcrap.

Microsoft, please learn to trust your customer base a little bit more.
