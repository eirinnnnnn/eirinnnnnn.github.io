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
![Alt text describing figure](/assets/img/DSPLab/01/block_diag_sigproc_flow.png)

carrier frequency $f_c=40$ kHz, signal bandwidth $f_w = \frac{1}{T_\mathrm{butst}} \simeq 5$ kHz

given a sampled received signal $x(t)$
- **Bandpass Filter**  

$$ x_\mathrm{bpf}(t) = x(t) * h_\mathrm{bpf}(t) $$

The choice of our bandpass fiter is the $6$ order iir butterworth. 
with the bandwidth (```HalfPowerFrequency```) to be $ f_c \pm 2f_w $ 

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

We perform the demodulation by

$$
x_\mathrm{de}(t) = x_\mathrm{bpf}(t) * e^{-j2\pi f_c t}
$$

Which in the frequency domain we can observe how the bandpass signal shifted to the baseband.

```matlab
w0 = 2*pi*fc/Fs;
lo = exp(-1j*w0*n);
bb = rx_bp .* lo;   
```

- **Lowpass Filter**

We pass the signal through a lowpass filter after demodulation.

```matlab
% FIR: passband up to lp_fc, stopband starts at 1.6*lp_fc
dlp = designfilt('lowpassfir', ...
    'PassbandFrequency', lp_fc, ...
    'StopbandFrequency', 1.6*lp_fc, ...
    'PassbandRipple', 0.1, ...          % ~±0.05 dB
    'StopbandAttenuation', 70, ...
    'SampleRate', Fs);

bb_f = filtfilt(dlp, real(bb)) + 1j*filtfilt(dlp, imag(bb));
```


- **Envelope**  

Since our signal is carried by $f_c$, we can model it as

$$
x(t) = A\cos(2\pi f_c t + \phi)
$$

In the demodulation we have the real part

$$
    \mathrm{Re}\{x_\mathrm{de}(t)\} = x(t)\cos(2\pi f_c t) = \frac{A}{2} (\cos(\phi) + \cos(4\pi f_c t + \phi))
$$

We can see the amplitude was halved.

So when taking the envelope we put a gain on it to compensate for the gain loss by 

```matlab
env  = 2*abs(bb_f);
```


And this is how we retrieve back this beautiful curve!


![bandpass signal vs. envelope](/assets/img/DSPLab/01/bp_env.png)

### Error analysis and correction term

By plotting out the difference of the number of samples $\Delta n$ between the measured and the theoretical value,


![Delta_n vs. distance](/assets/img/DSPLab/01/delta_n_dist.png)

We see that it is almost a linear model where the error decrease as the distance increase. Thus we choose to use a linear correction model as a function of $n_\mathrm{meas}$,

$$
 \Delta = a + b n_\mathrm{meas}
$$

We use a linear regression to fit the data and have $a\simeq53.14,\;b\simeq-0.02469$


The followig try to address the source of the error. 

- wavefront & peak
- wavepacket & distance