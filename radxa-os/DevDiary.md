**7/20/2025**
Today was terrible. 
Tried to get some hands on time with the Armbian OS and set up some directories in the Git repo. I was able to submit a few basic commands for git setting up the directory for the os along with the customize-image.sh to inject the armbian build into and readme file.
I progressed quickly into the next phase but ran into my first roadblock. the Armbian build system it self as i need to install armbian into a system. The suggestion from Chatgpt was to run a baremetal or VM of Ubuntu 20.04. I am low on space on my hard drives
and wanted to leverage oracles free offering with ampere. Oracle had other plans as they have denied all my credit and debit cards citing the information does not match when it clearly does. I cant create an account yet and thus cant use the VMs.
<img width="800" height="774" alt="image" src="https://github.com/user-attachments/assets/cbe2185e-8517-46f0-83d8-43f687386c63" />

I said ok fine, thats ok we will just use the Radxa it self and take this opportunity to install the OS directly on the board. At first I assumed it was a simple format the SD and flash an Armbian image to said card. I was wrong again. Linux storage is 
basically unreadble to a windows machine and spent an hour assuming i was sold a faulty sd card that was quickly losing space. The BalenaEtcher program was creating paritionns and I needed to downlaod another program, in this case an SD card formatting tool
to format the SD card and then install the image. 
<img width="469" height="525" alt="image" src="https://github.com/user-attachments/assets/620a742f-d1ce-46cf-896e-1b55ba9c143a" />

Fixed? Nope. I found out through trial and error that I not only possible ruined my Debian install but the OS was running off the eMMC (Embedded Multi Media Card) on board the PCB. Ok so I need to figure out how to flash that and get the Armbian community image on it.
Fine ok that doesnt seem impossible. After digging through documentation and trial and error I eventually reached this screen. 
<img width="1207" height="562" alt="image" src="https://github.com/user-attachments/assets/20c9f32b-b008-47b1-8756-c7b979a04641" />

I am unsure how to progress as every time I try to load an image on this eMMC it fails. I think I have an option to just wipe the eMMC and get the Radxa to boot direcrtly from the SD card. feels like I wasted all this time today for basically no movement.
Fuck. 

**7/22/2025**
I was able to format the SD card again and put Radxa's debian. I was able to let it boot back up which was great and testing out a few functions. I quickly found out the wifi connection does not work with the Linux install for some reason. The wifi module works with my cellphone so this could be an issue with xfinity routers and or 2.4/5ghz frequency. This is also a problem talked about in the Radxa forums. After troubleshooting their solutions and nothing worked I stopped. That was yesterday but didnt log it due to nothing being done. Today I formated the hard drive and found a different Armbian install from the community. https://github.com/armbian/community/releases, searched for zero3 and  found an image. Was able to flash that on the SD card and boot the system. Well kinda. I am now stuck at a black screen with 

nearing the end of the entry I got this error:

Gave up waiting for root file system device.
Alert! UUID=d4221fb8-21ec-47aa-bab2-85a7a71865cf does not exist. 
Dropping to shell! 
(initramfs)

I am now stuck at trying to get past this screen from the information  before there is aline that references the check rootdelay= (did the system wait long enough)
Since I dont have a linux system i tried to use my windows system to open the SD card and modify the files but this is also a new problem as I am no longer able to detect the SD card on my windows machine. This may be from the armbian flash. I will try on my macbook later when i find the usb c to usb a converter. 

**7/24/2025**
I'm in. Yesterday was long between studyin for GRE, applyingn to jobs that I will probably not even be interviewed for and working on this. I narrowed down the problem to not having a single line in the armbianenv.txt file which was rootdelay=10. Yes that one line disabled me from running on the Zero. In order to do this I needed to download Ubuntu and have it booted off of one of my computers. Easy enough until in my haste I decided to make a Surface Go tablet my Linux computer. Appearently, its difficult to boot any usb on surface products. After trial and error I was able  to use the recovery boot options to force a restart and then force the computer to boot into Ubuntu. The SD card reader wasnt working on the tablet but I was lucky Surface Gos have a micro sd card slot under the kick stand. Once booted, I used the search function and found the armbianenv.txt and added "rootdelay=10" on the 5th line of the txt file. Swapped it over to the Radxa and managed to run it! I will need to update the files here to reflect not using the radxa-os and bonus, the fucking wifi works. 

Going to hammer out a few more things before I go work out. 
**Update**
I was able to bootstrapp a working flask api server on armbian and connect to it with my phone through http. It took a ton of work that I will go in detail with tomorrow after I am done studying and applying for jobs for now goodnight. 

