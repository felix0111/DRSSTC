# DRSSTC - WORK IN PROGRESS

<img src="https://github.com/user-attachments/assets/98e42ae9-a365-4b6a-a306-cb31d6c1659c" width="300">

This repo is just for documentation purposes of my private project regarding the construction of a Dual-Resonant-Tesla-Coil.  
Some connections, layouts, soldering practices etc. found in this documentation might be less than ideal, this is not meant to be used as an example on how to do things. Working with high voltages can be deadly, especially autotransformers without isolation transformers and tesla coils with a low resonant frequency. See also [skin effect](https://en.wikipedia.org/wiki/Skin_effect).

---

Everything basically started when I saw some videos of Tesla Coils on youtube. Specifically the Dual-Resonant and Vacuum-Tube Tesla Coil really sparked my interest.
So I wanted to make my own Tesla coil and thus I decided to just wind a secondary coil and then build everything upon that.  

Because the secondary coil normally has hundreds to thousands of turns, I used a lathe to wind magnet wire with a diameter of 0.04cm onto a sewer pipe (r=8cm, h=58cm).  
After around two hours ~1450 turns have been wound onto the pipe. This should be equal to about 729 meter of wire. After that, I sprayed the coil with clear varnish spray to reinforce and fixate the magnet wire onto the pipe.  

Then I constructed the base of the whole Tesla coil. I just used two thin wood boards separated by 4 wooden sticks.  
<img src="https://github.com/user-attachments/assets/eebd75e9-317b-444d-83da-b1b310d700f2" width="300">

For the primary coil I used some insulated wire I had laying around. 
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

After testing around and having fun with the Tesla coil, I built a completely new, more robust and feedback-capable driver. The following driver is basically the UD1.3b DRSSTC driver from [Steve Ward (reposted by Kaizer Power Electronics)](https://kaizerpowerelectronics.dk/tesla-coils/universal-driver-1-3b/) with some small additions like LEDs for showing the state of each Gate-Driver. An additional H-Bridge between Gate-Drivers and GDT allowed for more power.  
The supply voltages for the logic, Gate-Driver and H-Bridge come from the 3 buck converters. 5V, 9V and 18V respectively.  
<img src="https://github.com/user-attachments/assets/3f9f78fd-7fcd-470b-9985-c00ace5bc853" width="600">

The new driver also had an input for a PWM interrupter signal which enables/disables the GDT driver circuit. This is very useful for reducing the overall load on the primary coil H-Bridge as it only allows oscillations for a very short time.  
For generating the interrupter signal I built a handhheld PWM signal generator with variable duty cycle and frequency.  
<img src="https://github.com/user-attachments/assets/44cd6d25-1a12-461c-9610-bcf290102d52" width="400">

At this point a new and powerful IGBT H-Brige (CM75BU-12H) switched the primary coil.  
<img src="https://github.com/user-attachments/assets/462d847a-3c77-4a6b-96f6-f074dd235362" width="400">

The H-Bridge is mounted on a big heatsink from an old cooler I had laying around. Its probably overkill but it never got anywhere close to warm. A newly wound GDT (same ferrite core as before) is connected to the side of the H-Bridge, not for cooling purposes but just for practical reasons.  
<img src="https://github.com/user-attachments/assets/0aee1eed-ed56-40f9-aaf6-4fb5ed0ad7ae" width="1000">

The H-Bridge is supplied by a capacitor bank made up of multiple 400V 470uF low ESR electrolytic capacitors connected to a 1.2kV 100A three-phase rectifier. An autotransformer (specifications unknown) provides an adjustable (mains) voltage, necessary to not blow up everything all the time.  
<img src="https://github.com/user-attachments/assets/0b7107fa-f0fd-45c6-bbcb-86cbc91a9439" width="600">  
<img src="https://github.com/user-attachments/assets/09ff6351-9c8f-4efd-9a71-58c4c4ca7f25" width="500"><img src="https://github.com/user-attachments/assets/abed4421-1ddc-49f7-9921-b0a4d0bd2392" width="500">  
<img src="https://github.com/user-attachments/assets/e28ec7de-879b-43da-8e18-57512f332b4d" width="400">

The problem with this big autotransformer is that it sometimes trips the circuit breaker because of its huge inrush current. To fix this, I built a starter which puts a 3kOhm power resistor in series to the autotransformer for the first second.  
The circuit works by charging a capacitor which makes the LM311P comparator toggle a relay after a certain threshold. The relay then shorts the resistor.  
<img src="https://github.com/user-attachments/assets/6de5b74f-bb37-4249-8b5a-e60e144e18a2" width="400">

2 packages of 4 parallel 2kV 0.047uF capacitors are in series with the primary coil. The resulting total capacitance of 0.094uF seemed to bring the best results. I should probably solder them together at some point..  
<img src="https://github.com/user-attachments/assets/7b3c96eb-5ee9-404d-82b3-002ccd50e698" width="500">

The primary coil also got upgraded to a copper pipe with a diameter of 1cm. The fixtures for the pipe are 3D printed. Having a bare metal coil allows for finetuning the primary resonant frequency but also brings the risk of the secondary arcing to the primary.
To counteract this, I also added an additional pipe on the outer edge of the primary. This pipe is directly connected to ground.  
<img src="https://github.com/user-attachments/assets/ae027b5d-4b96-4669-932b-6b9aedc581db" width="500">

Two cascading current transformers (with each cascade having ~30 turns) provide a signal for the drivers "over current detection" and feedback for switching at the zero crossings of the primary. Zero crossing is absolutely necessary for high power switching as it reduces the losses of the H-Bridge to ideally zero.  
The cores for the current transformers are basically just a smaller version of the GDT core. B64290L0615 is the exact name of the ferrite core. Again, the permeability is important for correct functionality. Using a random core will likely give bad signals.  
<img src="https://github.com/user-attachments/assets/473522c6-8707-4c53-9e2e-0cbf2ecee373" width="500">

After some extensive testing at lower voltages, I just couldnt get the Tesla coil to run without an external feedback signal so I kept using the signal generator. At some point I pushed the supply voltage up to mains voltage (230V). With a triple breakout point the following picture was taken.  
(Note the LED lights at the upper right and the florescent lamp to the right of the Tesla coil lighting up from afar)  
<img src="https://github.com/user-attachments/assets/38627d2b-23d5-4764-b14e-95ea152d6352" width="600">

---

End result? The destruction of the beefy H-Bridge which I didnt even notice at first. Probably from the missing feedback and some other circuit errors.

---

After 2 years of frustration while trying to get the feedback to work (and some long breaks from this project), I built a new driver again. This time the Universal DRSSTC Driver 2.7 Rev C from [loneoceans.com](https://loneoceans.com/labs/ud27/) which also originates from Steve Ward.  
<img src="https://github.com/user-attachments/assets/7c58477c-972c-4426-9ae1-907cbdedfe25" width="600">
<img src="https://loneoceans.com/labs/ud27/UD27Cschematic.png" width="600">

This driver has a more robust zero crossing detection by using a high-speed comparator and also allows phase shifting the signal from the current transformer.  
To find the correct inductor I measured the waveform of the primary coil (blue) and the H-Bridge gate signal (yellow) and then just tested random inductors until the gates are switched at the zero crossing of the primary coil.  

<img src="https://github.com/user-attachments/assets/51d4b159-7228-4abc-b075-02ff6f203e07" width="500">  

No inductor, switching too late

<img src="https://github.com/user-attachments/assets/da62e0b6-6926-438f-aa02-9723609279d8" width="500">  

Inductor 1, switching too soon

<img src="https://github.com/user-attachments/assets/03442baa-5e4c-4852-8805-c2c36070b2aa" width="500">  

Inductor 2, switching exactly on the zero crossing

# WORK IN PROGRESS
