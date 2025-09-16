---
layout: default
title: OTFS with Zak transformation 
parent: Notes
nav_order: 2 
---

# OTFS

Motivation: high-mobile UE suffering doppler shifts and delay spreads. 
this makes the channel stable in the Delay-Doppler (DD) domain instead of the usual OFDM.

design flow:

- placing symbols on DD grid
- ISFFT transforming DD to T-F domain.
- multicarrier waveform in transmission
- Receiver demodulation

## Channel Model and the Twisted Conv

Since we are considering time-varying channel

$$
y(t) = \int \int h(\tau,\nu)x(t-\tau)e^{\jmath 2\pi\nu(t-\tau)}d\tau d\nu + w(t)
$$

when doing sampling on the channel we perform it on the DD grid

$$
h\left[\ell, m\right] \simeq h(\frac{\ell}{M\Delta f}, \frac{m}{NT})
$$

therefore the channel is 2D sampled 

$$
\sum_{\ell=0}{L-1}\sum_{m=-M}^{M} h[\ell, m]
$$

And therefore the effective channel is performing a **twisted convolution** on the transmit signal

$$
Y[\ell,\nu]
=\sum_{\ell'=0}^{N-1}\sum_{\nu'=0}^{M-1}
H[\ell',\nu']\;
X\!\big[{\ell-\ell'},\;{\nu-\nu'}\big]\;
\exp\!\Big\{\,j2\pi\,\frac{\nu'}{N}\,{\ell-\ell'}\Big\}
\;+\; W[\ell,\nu].
$$

this is quasi time-invariant

## Twisted convolution in group theory

## Sympletic Transform and Pulse-Shaping 

## Zak Transform