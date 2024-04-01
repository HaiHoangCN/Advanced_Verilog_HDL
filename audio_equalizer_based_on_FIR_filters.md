# Audio equalizer based on FIR filters

- Work with signals that previously have been converted to an electrical signal (using microphone + amplifier, an electric guitar, a processor).
- Audio signal is AC with many different frequencies.

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/ba0759ae-4bf6-4d2d-a665-dbc92be98344" height="350">

- Use different ADCs with different numbers of bits, or different sample rates.
- Analog Devices or Texas Instruments have specially designed ADC to acquire audio signals. This ADC has usually 24 bits of resolution and is designed to acquire signals at standard audio sampling rates like 44 ksps, 96 ksps or 192 ksps.
- These sample rates have been selected according to the bandwidth that the human ear can acquire, which starts at 20Hz to 20kHz.
- Nyquist theorem (>= twice of frequency to acquire a signal without data loss) so the lower frequency that an audio ADC can be acquired must be at least 40ksps.
- 
