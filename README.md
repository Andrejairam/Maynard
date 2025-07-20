# Maynard
Repo for augmented reality glasses project. 
Hey everyone,

**About Me:**
  My name is Andre Jairam. I've been out of work for as of today 1.5 years. I have a background in cloud computing with 7+ years at Microsoft as a TPM. I started this work back in 2014/2015 with a start-up called ARECA, which stands for Augmented Reality Embodied Conversational Agents. This was a project that added superimposed images onto your physical surroundings. I was inspired by the 3d camera from the Nintendo 3DS and Yelp's monocle app. I chose to focus on my college degree instead of the start-up. From there, I struggled to finish school and worked in Microsoft retail, writing white papers on different technologies. One of the papers leveraged the Intel Kaby Lake-G architecture. Paper got the attention of a partner at Microsoft Corporate, who gave me a chance to work in the cloud. Please be patient with my coding ability and really understand how to code Swift, Flutter, Radxa, and Armbian technologies. 

**Components**
**Radxa Zero 3W:**
  This project centers on utilizing the Radxa Zero 3W as a base. The 3W has a few notable features that made it attractive for this project. 
https://radxa.com/products/zeros/zero3w
    1. HDMI support: The Rockchip RK3566 SoC has a quad-core ARM processor that supports H.264/H.265 encoder up to 1080P@60fps. There is a micro HDMI port that we will use for the proof of concept. Future iterations will see this being removed for a better interface on a custom pcb. For now we will use an HDMI driver breakout board. 
    2. Wireless support: Core of this project is the wireless capabilities of IEEE 802.11 a/b/g/n/ac/ax or wifi 6. This board also has an onboard antenna that will be more than enough for us but options to extend the antenna connector. In future iterations, we should be able to leverage the Ansys HFSS antenna permiation simulation test that can show us the best area for when we create the physical headset/glasses. 
    3. USB support: for the proof of concept, we will leverage the USB Type-C interface, but as we move to creating a custom PCB we will find ways to leverage this interface for input controls. For the proof of concept we are going to use usb for power and programming the board.
    4. Camera support: There is a 22 pin MIPI CSI port that can support a 8 megapixel camera. 8mp camera isnt acceptable in todays standards but this will support gesture and hand tracking. for the proof of concept we can attach a camera for this purpose but this is a north star goal. The priority is getting all these parts working on conjunction. 

-
**Other components of this project include (but not limited to):**
-
**HDMI driver board and display:** We are using for the proof of concept a 0.71 inch AMOLED Display thati s 1920 x 1080p along with an accompnying driver board that uses an 81 pin LVDS connector for the display and has a micro hdmi port with a micro usb port for power. Unfortantely the original seller from ALIExpress no longer has this item up for sale but I found similiar sellers (https://www.aliexpress.us/item/3256804608852650.html?spm=a2g0o.productlist.main.2.5bbf4bffiCkUyG&algo_pvid=f3c750bf-aa61-450a-bd0c-7cb47c536c1d&algo_exp_id=f3c750bf-aa61-450a-bd0c-7cb47c536c1d-1&pdp_ext_f=%7B%22order%22%3A%221%22%2C%22eval%22%3A%221%22%7D&pdp_npi=4%40dis%21USD%21305.45%21232.14%21%21%21305.45%21232.14%21%402101eab017529074189411133eff8d%2112000030514778131%21sea%21US%216009569734%21X&curPageLogUid=BpU1OE6bMYaw&utparam-url=scene%3Asearch%7Cquery_from%3A)
<img width="800" height="1065" alt="image" src="https://github.com/user-attachments/assets/ea8a2107-c64b-476a-89fc-e0f03379235f" />
What I need to understand is the exact layout and reference schematics for the driver board. I only have a picture and scarce details this will be a WIP as we progress the project as we need to combine the driver board with the Radxa Zero 3W to mount on the headset. 

**90 Degree Right Angle Prism:** The HDMI panel, though small wont suffice for a transparent display. We will use techniques to reflect light in this case we will use a 10mm x 10mm x 10mm right angle prism. We are folding or redirecting the image path created by the LCD mentioned above. a quick example of this is google glass. 

**Plano-Convex Magnifying lens:** Once we are able to adequately redirect the light we need to then magnify the image as we are still project a 0.71 inch screen. Because of this we need to mount the lens around 25-30mm from the naked eye. Since we are not directly putting this lens infront of your eye we have more room to work. Going to use JiaTong 20mm diameter plano-convex lenses with a 15mm focal length. The material isnt glass but thats ok considering we are focused on a proof of concept and an MVP. in future iterations we can get glass lens with anti reflective coatings or even optical glass with AR coating. 

**Optical Combiner Element:** Finally once we have the lens assembly we can add a optical semi transparent mirrors as a budget friendly combiner. The combiner sits infront of your eye and behind the lends of the glasses. this will reflect the image magnified by the lens and be transparent enough to see past. Ideally we would need a similar 20mm x 20mm size with a 1mm thickness. The material is plastic with no AR coating and must be set at a 45 degree angle. 

**3d Printer:** for the enclosure and glasses, the great majority of the frame will be 3d printed. The only thing I cannot print would be the lenses themselves. Currently using a Bambu x1 Carbon. 
-
**Software include (but not limited to)**
-
Software wil be split into 3 main sections and will be the highlight of the Github repo. 

**Mobile App:** This will fit the flutter project and handle connecting to the Radxa Wi-Fi module, submitting Wi-Fi credentials as we need to establish the Radxa module as a access point and a pass through to maintain wireless capabilities. Triggering screen mirroring as this will be the core of how we replicate a screen on your glasses and guiding the replay kit setup on iOS. In the future we will add Live camera overlays in case you want to take pictures, video record, and stream along with a lower power option on the camera to perform gestures for the "hands free" approach. 

**Radxa Backend:** This will be a Python app that recieves request from the mobile app for connection and mirror start/stop. We will also use this to udpate systems for Wi-Fi and provide status endpoints. This will also incorporate video/camera streaming and gesture signals in the future. 

**Build Image:** This is a custom Armbian build support for a stripped down OS that we need to install packages to such as pre configured hostapd.conf, dnmasq.conf. and systemd services. We want to do this to keep things light weight but also make the OS purpose build to boot up and just accept wireless access from a host cellphone. Everything else aside fomr security is not needed.
