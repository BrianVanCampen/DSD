## Lab 1-3

We want to build an simple audio processor with the following functions

- volume control
- low-pass filter
- high-pass filter
- 
![afbeelding (1)](https://github.com/BrianVanCampen/DSD/assets/91600019/4b15da7b-58c7-4455-aa37-2ae44512dea0)


First build and audio loop which samples and plays back audio samples. 

Once this is build, develop a test bench to check correct operation.

Also use the Integrated Logic Analyser to check proper operation.

You can also use a external logic analyser to test your design.

Document your tests

Use this website: https://forum.digikey.com/t/i2s-pmod-quick-start-vhdl/13065

Or use this: 

A German scientist has used the I2S audio interface to transfer music samples into the FPGA for editing.

The operation is as follows: the music is sampled and sent serially over I2S to the FPGA and converted to a parallel sample for the left and right channels.
Then the samples from the left channel are sent to a low-pass IIR filter and those from the right channel to a high-pass IIR filter. So you hear a different version left and right through your headphones.
He developed this for a Lattice FPGA, with a clock signal of 16MHz.
His system, however, requires a 25MHz clock, to derive the necessary clocks that the I2S interface will control. For this he used a PLL to go from 16MHz to 25MHz.
You can find the code on Digitap: Lab1 projects
You can also download the VHDL code in a ZIP-file: https://github.com/YetAnotherElectronicsChannel/FPGA-Audio-IIR

![afbeelding](https://github.com/BrianVanCampen/DSD/assets/91600019/ee63a39d-23a7-4c0c-aa72-6da03cbb604b)


He uses the same audio-interface, so if we can get the proper signals outside our Basys3 board, all internal logic should work.

To change from the Lattice to the Basys3 we need to:

Change the output and input pins to our board within the XDC file.
    Look at the pins in the entity declaration and copy-paste them in the right location of the XDC
Change the clock from 16MHz (Lattice) to 100 MHz (Basys3)
    He uses a PLL to make a 25MHz signal. We will use the Clocking Wizards from the IP Catalog to make a 25MHz from our 100MHz clock. This will use one of the Multi Media Clock Management hardware blocks.

Rebuild the project for our FPGA board

Place the files (which sometimes appear as virtual hard disks) in a project and modify it to get the correct operation
Start a project with the name: <your_name>_DSP_FPGA
Save this directly to your C drive to avoid too long data paths
Add your own block to create a 25MHz clock and replace the original PLL. This is allowed with "Clocking Wizard IP" or with a "clock divider“
Check the RTL  schematic and try to analyze the operation of the project with the knowledge from the I2S interface
Adjust the components so that you can switch between high-pass and low-pass on both channels at the same time
Create a test bench for your circuit. Only check the signals that the FPGA sends out, you don't have to put incoming audio samples in the test bench
Synthesize, implement and create a bit-file that you send to your FPGA
Zip your entire project folder & upload your zipped folder

**Original**:

![afbeelding (2)](https://github.com/BrianVanCampen/DSD/assets/91600019/edea9a63-49f9-4c47-9bf5-4fd1e8db0da0)

![afbeelding (4)](https://github.com/BrianVanCampen/DSD/assets/91600019/07822952-cd1a-4c3b-964f-f25f510ebd44)


You immediately see the problem with the PLL.
Both the low-pass as the high-pass filter use the same block, but other coefficients.

**Adapted**

![afbeelding (5)](https://github.com/BrianVanCampen/DSD/assets/91600019/79682842-43ee-4e7e-9683-1b468830a65c)

![afbeelding (6)](https://github.com/BrianVanCampen/DSD/assets/91600019/aaf9cb33-3ee3-46ef-8d8f-35a00476070b)



Our own clock management has substitutes main_pll.

![afbeelding (7)](https://github.com/BrianVanCampen/DSD/assets/91600019/74154672-8742-4c1d-aea6-7ef060f68c42)

![afbeelding (8)](https://github.com/BrianVanCampen/DSD/assets/91600019/3a0f9f90-4dad-4fd3-92b6-e671ea6a3a2c)

![afbeelding (9)](https://github.com/BrianVanCampen/DSD/assets/91600019/e5176fa8-3729-4258-94d5-4295cb0fa67a)

![afbeelding (10)](https://github.com/BrianVanCampen/DSD/assets/91600019/7b627b52-d13d-4e42-a163-0ae1ce57903c)

![afbeelding (11)](https://github.com/BrianVanCampen/DSD/assets/91600019/dfeb2bec-a774-4fe2-88df-9007f0a9fb44)


We adapted the XDC.

![afbeelding (13)](https://github.com/BrianVanCampen/DSD/assets/91600019/e0522976-a40a-4812-b682-c3dd45ce68c8)

![afbeelding (14)](https://github.com/BrianVanCampen/DSD/assets/91600019/d35ff71f-3f39-43d4-a586-772caddafc22)

![afbeelding (12)](https://github.com/BrianVanCampen/DSD/assets/91600019/36aecd67-1245-4e7a-924b-267407b7f180)


Reference material:
https://reference.digilentinc.com/reference/pmod/pmodi2s2/start
https://reference.digilentinc.com/_media/basys3:basys3_rm.pdf


Develop an simple audio processor. Now we know how to sample music and get it into our FPGA, we would like to look at the effect of different audio procession blocks.

Develop a component for volume control with the switches
Use the component for a low pass audio filter
Use the component for a high pass audio filter
Develop a mux to choose: clean, low-pass, high-pass
Extra: Develop a component to perform a moving average filter on the signal

Reference material

https://github.com/Digilent/Pmod-I2S2
https://surf-vhdl.com/how-to-implement-moving-average-in-vhdl
https://www.fpga4student.com/2017/01/a-low-pass-fir-filter-in-vhdl.html

Rebuild the digital system using as IP blocks.

Start with using I2S IP to get audio samples in and out, without processing
Find a FIR filter component
Use the component for a low pass audio filter/ high pass filter

Reference material
https://www.cuidevices.com/blog/understanding-audio-frequency-range-in-audio-design
https://fiiir.com/
