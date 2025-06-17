# DRSSTC - WORK IN PROGRESS

This repo is just for documentation purposes of my private project regarding the construction of a Dual-Resonant-Tesla-Coil.  
Some connections, layouts, soldering practices etc. found in this documentation might be less than ideal, this is not meant to be used as an example on how to do things.  

---

Everything basically started when I saw some videos of Tesla Coils on youtube. Specifically the Dual-Resonant and Vacuum-Tube Tesla Coil really sparked my interest.
So I wanted to make my own Tesla coil and thus I decided to just wind a secondary coil and then build everything upon that.  

My father had an old lathe which I could use, the problem is that at its lowest setting it still rotated too fast. My idea was to use the clamps of the lathe to hold a stepper motor which will rotate the pipe. A custom 3D printed part connected the motor and the pipe.
The stepper motor was controlled by a dedicated stepper motor controller board in combination with an arduino and a potentiometer. Sadly I dont have any code or schematics regarding this circuit anymore, just a picture of the stepper motor.  
<img src="https://github.com/user-attachments/assets/065ae7b0-6344-4475-9713-63bef44d2d6d" width="300">

The support of the secondary coil is a sewer pipe with a radius of 8cm and height of 58cm. I decided to use magnet wire with a diameter of 0.04cm.
After around two hours ~1450 turns have been wound onto the pipe. This should be equal to about 729 meter of wire. After that, I sprayed the coil with clear varnish spray to reinforce and fixate the magnet wire onto the pipe.

After that, I constructed the base of the whole Tesla coil. I just used two thin wood boards separated by 4 wooden sticks.
<img src="https://github.com/user-attachments/assets/eebd75e9-317b-444d-83da-b1b310d700f2" width="300">

For the secondary coil I used some insulated wire I had laying around. 
No cats were harmed in the making of this coil!! :)  
<img src="https://github.com/user-attachments/assets/8aaca457-dc67-4f6c-a0ea-3e8ae3afca29" width="700">
<img src="https://github.com/user-attachments/assets/15d911c9-518f-4f77-ab18-4410c84a854a" width="400">

The topload is just a piece of flexible aluminum duct.  
<img src="https://github.com/user-attachments/assets/2bf020bf-ed73-4cd9-889f-ac2920f95573" width="400">

The next picture shows a prototype of the Gate Drive Transformer (GDT) and its controller. The GDTs core (B64290L0048) is a ferrite core toroid. Note that the permeability is important for a correct signal transmission at switching frequencies.
Here the GDT is directly switched by two UCC27423 Gate-Drivers. These are typically used to switch MOSFETs and IGBTs but to some extend can also be used for GDTs.  
I wonder how that circuit even worked looking like this. :)  
<img src="https://github.com/user-attachments/assets/8d455fdd-2c2d-4078-9daa-112dd274587d" width="500">

The MOSFETs which were used to switch the primary coil are shown in the next picture. Again, I dont really know how that circuit worked, just that there are two MOSFETs (probably IRFP460) each with their own signal pair for faster and high power switching.  
<img src="https://github.com/user-attachments/assets/a2cefcbe-5514-4c6f-a223-af51145cf007" width="500">

At this point, there was no feedback in any way so I used a cheap signal generator for generating a PWM signal which basically defines the switching frequency of the primary coil. I dont remember the supply voltages but they were close to the maximum supply voltage of the UCC27423 and the maximum Drain-Source voltage of the MOSFETs.
I found that at a frequency of 125kHz, the sparks were the biggest which hints to a secondary resonant frequency of around 125kHz. The breakout point is just a big wood screw leaning against the topload.  
<img src="https://github.com/user-attachments/assets/4b07cd5a-52c4-4e1b-8f63-08333e77891e" width="500"><img src="https://github.com/user-attachments/assets/99589b24-f95f-477a-ba6b-7aae404a2fc1" width="500">

After testing around and having fun with the Tesla coil, I built a completely new, more robust and feedback-capable driver. The following driver is basically the UD1.3b DRSSTC driver from Steve Ward with some small additions like LEDs for showing the state of each Gate-Driver. An additional H-Bridge between Gate-Drivers and GDT allowed for more power.  
The supply voltages for the logic, Gate-Driver and H-Bridge come from the 3 buck converters. 5V, 9V and 18V respectively.  
<img src="https://github.com/user-attachments/assets/3f9f78fd-7fcd-470b-9985-c00ace5bc853" width="600">

At this point a new and powerful IGBT H-Brige (CM75BU-12H) switched the primary coil.  
<img src="https://github.com/user-attachments/assets/462d847a-3c77-4a6b-96f6-f074dd235362" width="400">

The H-Bridge is mounted on a big heatsink from an old cooler I had laying around. Its probably overkill but it never got anywhere close to warm. A newly wound GDT (same ferrite core as before) is connected to the side of the H-Bridge, not for cooling purposes but just for practical reasons.  
<img src="https://github.com/user-attachments/assets/0aee1eed-ed56-40f9-aaf6-4fb5ed0ad7ae" width="1000">

The H-Bridge is supplied by a capacitor bank made up of multiple 400V 470uF low ESR electrolytic capacitors connected to a 1.2kV 100A three-phase rectifier. An autotransformer (specifications unknown) provides an adjustable (mains) voltage, necessary to not blow up everything all the time.  
<img src="https://github.com/user-attachments/assets/0b7107fa-f0fd-45c6-bbcb-86cbc91a9439" width="600">  
<img src="https://github.com/user-attachments/assets/09ff6351-9c8f-4efd-9a71-58c4c4ca7f25" width="500"><img src="https://github.com/user-attachments/assets/abed4421-1ddc-49f7-9921-b0a4d0bd2392" width="500">  
<img src="https://github.com/user-attachments/assets/e28ec7de-879b-43da-8e18-57512f332b4d" width="400">

2 packages of 4 parallel 2kV 0.047uF capacitors are in series with the primary coil. The resulting total capacitance of 0.094uF seemed to bring the best results. I should probably solder them together at some point..  
<img src="https://github.com/user-attachments/assets/7b3c96eb-5ee9-404d-82b3-002ccd50e698" width="500">

The primary coil also got upgraded to a copper pipe with a diameter of 1cm. The fixtures for the pipe are 3D printed. Having a bare metal coil allows for finetuning the primary resonant frequency but also brings the risk of the secondary arcing to the primary.
To counteract this, I also added an additional pipe on the outer edge of the primary. This pipe is directly connected to ground.
<img src="https://github.com/user-attachments/assets/ae027b5d-4b96-4669-932b-6b9aedc581db" width="500">

Two cascading current transformers (with each cascade having ~30 turns) provide a signal for the drivers "over current detection" and feedback for switching at the zero crossings of the oscillation. Zero crossing is absolutely necessary for high power switching as it reduces the losses of the H-Bridge to ideally zero (and I think it increases the lifetime).  
The cores for the current transformers are basically just a smaller version of the GDT core. B64290L0615 is the exact name of the ferrite core. Again, the permeability is important for correct functionality. Using a random core will likely give bad signals.
<img src="https://github.com/user-attachments/assets/473522c6-8707-4c53-9e2e-0cbf2ecee373" width="500">

After some extensive testing at lower voltages, I just couldnt get the Tesla coil to run without an external feedback signal so I kept using the signal generator. At some point I pushed the supply voltage up to mains voltage (230V). With a triple breakout point the following picture was taken.  
(Note the LED lights at the upper right and the florescent lamp to the right of the Tesla coil lighting up from afar)  
<img src="https://github.com/user-attachments/assets/38627d2b-23d5-4764-b14e-95ea152d6352" width="600">

---

End result? The destruction of the beefy H-Bridge which I didnt even notice at first. Probably from the missing feedback and some other circuit errors.

---

After 2 years of frustration while trying to get the feedback to work (and some long breaks from this project), I built a new driver again. This time the Universal DRSSTC Driver 2.7 Rev C from [loneoceans.com](https://loneoceans.com/labs/ud27/) which also originates from Steve Ward. 
# WORK IN PROGRESS
