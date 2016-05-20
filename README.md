##  A Software Introduction to West Coast Modular Synthesis

by Chris Holder email chris.holder@mail.com 

The aim of this project is to provide a cost effective introduction into modular type synthesis for novice users. The software component provides an insight into the sonic capabilities of modular synths and offers an overview of some of the key techniques used by the practitioners of these units such as Morton Subtonick who wrote the classic Silver Apples of the Moon. Released in 1967, it was the very first electronic music ever commissioned by a record label and also Alessandro Cortini of Nine Inch Nails (some of these techniques are shown in the accompanying demonstration video the link for this and the Pure Data software for this project can be found at the bottom of the page).

The software for this project is a physical model of the Buchla 258 Dual oscillator (shown in fig 1). This unit created the main tonal capabilities of the early Buchla modular system. When this model is used in conjunction with a couple of other modular units, the powerful sonic capabilities of this type of synthesis soon become apparent. The 258 dual oscillator dates from the early 1970’s the main reason to physically model such an old system is due to the lack of complexity of control in comparison with the modern versions of these models. 
 

![buchla258](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-02-22%20at%2021.26.35.png)

**fig 1** the 258 dual oscillator










##The long and winding road (of development)


To begin physically modeling this unit the first consideration was based upon the photograph in fig 1 which shows the fascia of the physical unit. From this photograph we can deduce that a potentiometer is being used to control the frequency output by the unit. Another potentiometer (“pot”) is being used to control a trimming of the frequency output (shown in fig 2). From the screen shot of the Pure Data abstraction (Fig 2) is showing how the software slider is being used to manipulate the output of the sine and square oscillators OSC~ and SQUARE~ objects in the screenshot. One pot is being used to control the wave shape of the unit from sine to saw and sine to square wave at this stage in the development however this function had not yet been implemented. The remaining three pots are being used to control the amount of audio signal being introduced to the frequency modulation (FM) circuit and the amount of modulation for 2 separate FM circuit designs (shown in fig 3).      

![donscreen1](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-04-28%20at%2015.04.38.png)

**Fig 2** shows the application of Pure Data to realize the frequency functions

In the screenshot Fig3 is shown how a slider labeled FM in has been used to manipulate the amplitude of audio being input into the FM circuit by using the *~ object. The FM lin and FM exp sliders are being used to manipulate the amount of modulation affecting the audio input this also utilizes the *~ object.

 ![don2screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-04-28%20at%2015.05.24.png)
      
**Fig 3** shows the starting implementation of Frequency modulation in Pure Data.

The final parts on the unit fascia with ref to fig 2 to consider was the input and output jack sockets but at this stage in the project these were ignored till the main functions of the unit had been realised.

On the physical Buchla 258 unit the wave shaper function slides very smoothly between the offered waveforms, however achieving this smooth transgression in Pure Data was a troublesome process. The first attempts at this functionality were clunky at best and missed many of the sonic points that the Buchla unit was effortlessly capable of. After searching the Internet a forum known as Muff Wiggler that has many members with Circuit diagrams for these old modular units. Using this circuit diagram the relevant part of the circuit is shown in Fig 4, from this diagram it was deduced that the two different wave shapes are summed together thought an operational amplifier, which by its nature of operation mixes two signals depending on their respective voltage levels. This operation was then mimicked in Pure Data by inverting the output of sliders controlling the amplitude of each signal (shown in Fig 5). 

![don3screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-04-29%20at%2016.03.37.png)

**Fig 4** Circuit diagram showing output Operational Amplifier 1973.

![don4screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-04-29%20at%2016.35.12.png)

**Fig 5** Pure Data screenshot showing inverted slider 

This inversion allows for a smooth transition between the two waveforms with this achieved the main user interactive parts of the device where successfully replicated in a software environment. 
The next part of this project began with exploring different ways to make the jack socket inputs and outputs of the unit in a software environment intuitive.
The first idea for this operation was to use the link system by which Pure Data connects different objects together to mimic “patching” to different inputs and outputs (shown in Fig 6). However this attempt failed due to Pure Data’s DSP loop detection not allowing an input and output being connected from the same abstraction. 
 
 
![don4screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-02%20at%2010.49.48.png)
  
  **Fig 6** Shows the failed attempt to map the various 
jack socket operations. 

From this failed attempt came the idea to use the Toggle object within Pure Data, which is a simple switch to imitate plugging in the jack leads. However this idea does come with one drawback that being for every connection to be made must be represented by a different toggle object. Despite this one draw back the method was used as being the next most intuitive system to mimic the “patching” used by modular synthesizer systems. 

The next task of this project was to look into the operation of each input for the system. These inputs are the Control voltage inputs and the 1-volt per octave system implemented by Moog in the early 1970’s. The original Buchla system for pitch tracking was a volt per hertz system however this meant that fewer octaves could be expressed over a given voltage range (Dalgleish 2016). However over the intervening years Moog’s system became the more popular method for tracking pitch on modular systems (Dalgleish 2016). Hence this method was used for greater compatibility should the unit be made into a digital hardware version. The Control voltage and one volt per octave system that was implemented within the software for this project (shown in Fig 7), functions by scaling midi note values into the modeled working voltage of a modular synth in this case +5 and -5 volts. Once this scale has been done the output is turned into a scaled floating signal. The signals amplitude is then increased by a value of 5 to ensure a positive value this in turn is then multiplied by 12 to restore the 0-120 midi note values. The reason for then subtracting by 60 is to scale the pitch into 6 octaves this control signal is then turn into frequency to drive the tone generation oscillators. With the CV and 1 volt octave system in place the unit now had all the major functions available on the Buchla 258. The final phase of this project was to begin making the software abstraction have authentic Buchla audio output.

![don4screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-02%20at%2012.40.26.png)

**Fig 7** shows the 1volt per octave scaling to control modeled voltage output. 


With an aim to get the software as authentic as possible to the original unit, the software audio output was compared to a Youtube demonstration of a homemade clone version of the 258. With this juxtaposition it was discovered that the exponential FM output sounded completely different to that of the hardware version, even taking into account factors such as amplification warming the sound, the microphone or mobile phone used to record the video colouring the sound did not accommodate the difference in sound. Upon investigation it was discovered that what Buchla described as exponential FM is also known as cross modulation (Timoney et al 2011). With this new routing in place the software was starting to get a lot closer to the original sound of these units. 

Historically synthesizers suffered from a problem with heat causing the electronic circuit to drift in pitch. Hence most old synthesizers came with a trim or tuning button to retune the instrument when this occurred. To model this aspect in Pure Data a stochastic probability model was used (shown in fig 8). This type of random probability is based upon a dice roll (Taylor et al 1994 p66). 



![don4screen](https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-02%20at%2016.12.19.png)

**Fig 8**  A stochastic probability abstraction.

The stochastic abstraction works by setting a random start time from the loading of the patch this emulates the device being turned on and the circuits starting to warm. After the initial load-bang the time for the drift to occur is then random set to bang the dice roll to determine how far the unit will drift controlled by the rule set applied to the die from plus or minus 1 midi note up to 3 midi notes value in drift. 
The Buchla series of modular synthesizers always had a distinctive sound this was caused by Don Buchlas use vactrols in his circuit designs by having a non-linear response to amplitude changes. From the circuit diagram of the 258 (shown in Fig 9) the vactrol IC is being used to control the modulation capabilities of the unit.

![don4screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-03%20at%2011.56.41.png)

**Fig 9** Vactrol IC from Buchla 258.

A Vactrol is basically a light dependant resistor, the more light that shines on it, the more voltage runs through it. You could typically hook one of these up to anything you may be circuit bending and use your hand to block out the light to modify the voyage. The Vactrol equation in this case, uses heat to drive the LED this then slows down the response to incoming control signals through a complex nonlinear filter. To emulate this response in Pure Data I used an open source abstraction (shown in Fig 10). The output of the LOP object is scaled nonlinearly by the mathematical power expression the sum of this signal is then added to the original signal taking the maximum value of the combined inputs for its output. Non-linearity is then enforced by the Max~ object outputting the peak value of the signal. 

 ![don5screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-03%20at%2011.25.28.png)
 
 **fig 10** shows the Pure Data open source abstraction of a vactrol.
 
##  Software Overview

The graphic user interface or GUI for the 258 dual oscillator emulation software, (shown in Fig 11) “IDON” has been designed to provide easy navigation around the control mechanism whilst at the same time aimed at giving an intuitive modular feel and to maintain an authentic look to the software. 
 
 ![don6screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-03%20at%2013.24.16.png)
 
 **fig 11** shows the GUI of the 258 Dual Oscillator.
 
 
 Due to the nature of modular synthesis one single unit on its own would be musically not very useful and many of the patching techniques involved in modular synthesis would not be possible. Therefore the 258 Dual oscillator comes with 3 additional Pure Data patches to make this software fully capable.
The first of these patches is a model of the Buchla 123 sequential voltage source the original is shown in fig 12 with the software abstraction (fig 13) shown further below these images are juxtaposed to show the attempt at authenticity of the GUI. 



 ![don6screen] (https://github.com/s1thlord/idon/blob/gh-pages/6979195532_f56baf3a3f_b.jpg)
 
 **fig 12** Buchla step sequencer 123 model
 
 ![don7screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-18%20at%2017.26.30.png)
 
 **fig 13** Software GUI step sequencer.
 
 Keeping with the 1970’s flavor of the project it was considered to also model The Buchla 280 quad envelope generator shown in Fig 14 with the Pure Data version shown below (fig 15). With the addition of these two units the oscillator model becomes controllable in terms of pitch manipulation and also note on and off control via the envelope generator. 
 
 ![don8screen] (https://github.com/s1thlord/idon/blob/gh-pages/buchla28007.png)

 **fig 14** Buchla Quad envelope generator.

 ![don9screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-18%20at%2017.30.36.png)
 
 **fig 15** Pure Data software GUI Envelope Generator.
 
 The final patch is a simple audio volume controller or mixer design to give complete control over the audio outputs no Buchla reference was used for this patch (shown in fig 16).
 
 
  ![don10screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-18%20at%2017.36.12.png)

 **fig 16** shows GUI of Pure Data volume controller.
 
##   User Guide to the software 

This simple user guide is here to explain the very basic operation of the Pure data patches for a full working demonstration please see the video link at the bottom of this page. 

To operate this project it is recommended that all four patches are fully loaded before beginning. Once all four patches are loaded simply push up the required oscillator volume slider, coloured blue in the mixer patch (shown in Fig 16). From here it is a simple matter of crafting a desired sound from the oscillator by turning the frequency control. The technique known as patching is achieved by using the toggles on the GUI, shown in Fig 17 as a quick example to patch the pitch voltage to the 1 volt per octave input you have to depress both toggles coloured green in this case for the signal to flow between the units it is hoped that this design simulates placing a jack lead between the inputs and outputs of the various units.

 ![don11screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-18%20at%2017.37.38.png)

**Fig 17** screen shot showing patching toggles.

The patching process for the 258 model is achieved in the similar manner as the previous example. With reference to fig 17 to patch the control voltage over the Frequency controller you would simply press the desired wave shape toggle located just above the frequency dial. In this case only the one toggle needs to be activated. The reason for the single toggle patching process for this unit was to make the GUI less cluttered and easier to understand. 
  
  ![don11screen] (https://github.com/s1thlord/idon/blob/gh-pages/Screen%20Shot%202016-05-18%20at%2017.37.51.png)
  
  **Fig 18** Screenshot showing software input toggles on 258 model.


This user guide is meant to cover only the very basics of the software
It is strongly advised for any new comers to this type of synthesis to watch the demonstration video accompanying the software (link at bottom of page). 



## Resources

Dalgleish, M   The Modular Synthesizer Divided Econtact web page, 2016. available at http://econtact.ca/17_4/dalgleish_keyboard.html

Vactrol Pure data abstraction:  available at https://github.com/wilsontr/pd-abs

Timoney. J, Lazzarini. V Exponential Frequency Modulation Bandwidth Criterion For Virtual Analog applications 2011 available at: http://recherche.ircam.fr/pub/dafx11/Papers/60_e.pdf  


 Howard M. Taylor, Samuel Karlin An Introduction to Stochastic Modeling
  Academic Press. 1996. London 


Any comments or enquiries about the software please e-mail the author chris.holder@mail.com

## Tutorial video link
https://youtu.be/1ptTxy4Khcs


## software download
**Sequencer:**
 https://github.com/s1thlord/idon/blob/gh-pages/buchla%20123.pd 
 
 **Audio mixer:**https://github.com/s1thlord/idon/blob/gh-pages/buchla%20mixer.pd            

**Quad gate:** https://github.com/s1thlord/idon/blob/gh-pages/buchla%20280.pd

**Oscillator:** https://github.com/s1thlord/idon/blob/gh-pages/buchla258s.pd
