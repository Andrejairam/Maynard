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

