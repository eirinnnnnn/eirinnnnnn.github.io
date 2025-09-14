---
layout: default
title: DSPLab 
parent: Notes
nav_order: 1 
---


# DSPLab (NYCU 2025Fall)

## Lab1 (Ultrasound Module & signal processings)

### Hardware spec

### Signal Processing

Ultrasound Module Received signal data processing:
![Alt text describing figure](/assets/img/block_diag_sigproc_flow.png)

carrier frequency $f_c=40$ kHz, signal bandwidth $f_w = \frac{1}{T_\mathrm{butst}} \simeq 5$ kHz

given a sampled received signal $x(t)$
- **Bandpass Filter**  
$$
x_\mathrm{bpf}(t) = x(t) * h_\mathrm{bpf}(t)
$$
The choice of our bandpass fiter is the $6$ order iir butterworth. 
with the bandwidth (```HalfPowerFrequency```) to be $f_c \pm 2f_w$ 
```matlab
bp_bw = max(2*fw, 12e3);            
bp_f1 = max(10, fc - bp_bw);           
bp_f2 = min(Fs/2-10, fc + bp_bw);      
dbp = designfilt('bandpassiir','FilterOrder',6, ...
    'HalfPowerFrequency1',bp_f1,'HalfPowerFrequency2',bp_f2, ...
    'SampleRate',Fs);
rx_bp = filtfilt(dbp, rx_dc);  
```

- **Demodulation**  

$$

$$

- **Lowpass Filter**
- **Envelope**  
