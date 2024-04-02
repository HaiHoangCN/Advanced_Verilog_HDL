# Audio equalizer based on FIR filters

- Work with signals that previously have been converted to an electrical signal (using microphone + amplifier, an electric guitar, a processor).
- Audio signal is AC with many different frequencies.

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/ba0759ae-4bf6-4d2d-a665-dbc92be98344" height="350">

- Use different ADCs with different numbers of bits, or different sample rates.
- Analog Devices or Texas Instruments have specially designed ADC to acquire audio signals. This ADC has usually 24 bits of resolution and is designed to acquire signals at standard audio sampling rates like 44 ksps, 96 ksps or 192 ksps.
- These sample rates have been selected according to the bandwidth that the human ear can acquire, which starts at 20Hz to 20kHz.
- Nyquist theorem (>= twice of frequency to acquire a signal without data loss) so the lower frequency that an audio ADC can be acquired must be at least 40ksps.
- 

# Keywords from https://www.controlpaths.com/2021/06/28/audio-equalizer-based-on-fir-filters/
- ADC, DAC
- Resolution of ADC
- Sampling rate [ksps, sps]
- Bandwidth
- Nyquist theorem
- Data loss
- Digilent’s PMOS I2S2
- a Cirrus ADC CS5343
- a DAC Cirrus CS4344
- Inter IC Sound (I2S)
- system clock (MCLK)
- delta-sigma modulator/demodulator
- clock for the communication (SCLK)
- clock that is corresponding with the sample rate (LRCK)
- data signal (DATA)
- stereo signals
- double data rate (DDR) signal
- the LRCK signal
- prescaler logic
- AXI4-Stream protocol
- data width
- dataL + 8 bit padding + dataR + 8 bit padding
- 3-band equalizer
- low frequencies for the woofer and high frequencies for the tweeters
- the Bass band, for frequencies between 1Hz and 800Hz, the Medium band for frequencies between 800Hz and 3000Hz, and the Treble band for frequencies between 3000Hz and 8000Hz
- harmonics
- DFT
- filters like FIR or IIR (split the signal)
- real-time audio processing
- group delay
- spectral phase of the filter
- linear phase system
- distortion in the audio signal
- narrow band equalizer
- high-order filter
- design the filters using Python
- high cross-band between filters?
- Regarding the design of the filters, they are designed with 33 "taps", and for the bass and mid, I have used "a square window" to improve the attenuation. This will cause a "ripple" in the mid-band. For the treble band, I used "a Hanning window".
- symmetric FIR filter
- 16 coefficient inputs to implement a 32nd order FIR filter
- I2S transmitter and receiver

# Introduction to ADC and DAC
Link: https://www.youtube.com/watch?v=HicZcgdGxZY&list=PLwjK_iyK4LLCnW-df-_53d-6yYrGb9zZc
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/6fb1b9b3-01ec-4df4-af2b-775454a6ad7a" height="300">
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/e2a30d71-dba3-42ef-a1b1-7aecc1f3430b" height="300">
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/6ee3bd5c-e6e2-4f03-9430-336d5a7f2934" height="60">

Analog Signal:
- Susceptible to Noise
- Difficult to Process in Analog Domain
- Difficult to Store in Analog Domain

Digital Signal:
- Less susceptible to Noise
- Easy to Process in Analog Domain
- Easy to Store in Analog Domain

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/679ab24f-e2de-4399-8a2f-c907cdaef11d" height="75">

Analog Signal is continuous in time & amplitude.

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/cd5948db-28da-4f2d-9b5f-93531c2e04ea" height="300">

**Quantization**: Process of assigning a sampled signal a value from the discrete set of values.

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/bffa6556-f46d-4697-b604-88618c6db952" height="300">
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/bf751143-1e27-47df-b383-68a99e331c62" height="150">
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/d8b5aa27-f812-42d8-b0a7-6bcb7c91abf7" height="300">
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/8b18ba6a-0bd8-4e81-9f2d-1eb421e33d09" height="300">

