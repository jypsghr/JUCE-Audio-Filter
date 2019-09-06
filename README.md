# JUCE-Audio-Filter
Audio filtering plugin using the JUCE framework using FIR, IIR, Butterworth and Biquad filters.

![Alt text](https://github.com/MattH96/JUCE-Audio-Filter/blob/master/Filter.png?raw=true "Filter GUI")

TO USE:
Simply place the .vst3 file into a digital audio workstation, I recommend Reaper but Garage Band, Ableton, and a variety of other DAWs work just fine.
Run a sound file through it and you can test out the algorithmns. 

TO COMPILE:
Download the JUCE framework, it's an industry go-to for audio application development, I highly reccomend it!
Open the given JUCER file and click 'Open in IDE', build the project and then you can get the .vst3 file from the builds folder. 
By using the JUCER file you can change the file output types and change a variety of other application parameters to best fit your needs.

A BIT ABOOUT THE CODE:
The Filter.cpp and Filter.h file is the complete filtering library. To use the filter for real time audio applications construct it like so:

Constructor - MyFilter filter[NUM_CHANNELS]  
Before playback begins - filter[channel].prepareToPlay(sampleRate, samplesPerBlock)

FIR/IIR filter types use:  
outputData[sample] = filter[channel].FIR_IIR_Filter_Method_In_Class(inputSample, frequency)  
NOTE: FIR/IIR filters use (Frequency/2000) * 0.49 as frequency.

Biquad/Butterworth filter types use:  
filter[channel].setBiquad/Butter(filterType, frequency, Q, peakGain)  
outputData[sample] = filter[channel].processBiquad/Butter(inputSample)

NOTE: frequency is true frequency in Hz, 20-20000.  
NOTE2: There is a known issue that causes the Biquad filter to clip and mute the channel when first changing to the Biquad filter type, I haven't been able to find the error but pausing the audio and unmuting resolves this issue, the issue is not replicated after the first clipping error.
  
For non-real time filtering the process is similar.

The FastMath.h library is currently not in use but does do some great fast mathematics function approximations, feel free to steal this and use it whereever you see fit.  
The remaining source code is audio generated by the JUCE framework and built upon, see the JUCE website and TheAudioProgrammer's youtube for some great tutorials.

Thanks for checking this out!   
Matt
