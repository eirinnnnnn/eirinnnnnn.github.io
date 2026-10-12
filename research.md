---
layout: default
title: Research
nav_order: 3
---

# Research

I work on coding theory with [Prof. Yu-Chih (Jerry) Huang](https://sites.google.com/site/ycjerryhuang/) at NYCU. Most of it sits where algebra meets decoding: take a classical binary linear block code (BCH, Golay, Reed–Muller) and ask how much of its structure a polar-style successive cancellation decoder can be made to use.

**Interests:** information and coding theory, the algebraic structure of polar and Reed–Muller codes, structured decoding algorithms, and the places where coding theory meets theoretical computer science.

## Papers

1. **Pin-Jing Li** and Yu-Chih Huang, "Parallel decoding of binary linear block codes via equivalent polar transformation class," *IEEE Information Theory Workshop (ITW)*, Nov. 2026, to appear. [[arXiv]](https://arxiv.org/abs/2601.11373) [[code]](https://github.com/eirinnnnnn/POD)
2. **Pin-Jing Li** and Yu-Chih Huang, "Early selection of polar ensemble decoding with successive cancellation style component decoder," in preparation.
3. **Pin-Jing Li** and Yu-Chih Huang, "Successive cancellation permutation decoding of eBCH as Reed–Muller code sandwich," in preparation.

## Talks and posters

- "Parallel decoding of binary linear block codes via equivalent polar transformation class," IEEE Information Theory Workshop (ITW), Arizona, USA, Nov. 2026 (upcoming).
- "Polar ensemble decoding of binary linear block codes," poster, IEEE East Asian School of Information Theory (EASIT), Hsinchu, Taiwan, Jul. 2026. **Poster Award.** [[poster]](./assets/pdf/easit2026_poster_ped.pdf)

---

## Polar ensemble decoding

*2025 to now, paper 1.*

The universal decoding framework of [Lin et al.](https://doi.org/10.1109/OJCOMS.2020.2979529) permutes the coordinates of any binary linear block code so that it becomes a polar subcode with dynamic frozen bits, which lets a single polar decoder serve many code families. The catch is that its decoder, successive cancellation list (SCL) decoding, is sequential. The usual way to parallelize polar-like decoding, automorphism ensemble decoding, is built one code family at a time and relies on static frozen sets, so it does not carry over.

Polar ensemble decoding (PED) gets around this by letting the automorphism group of the code act on the *transformation parameter*, that is, on the permutation, instead of on the codewords. All permutations in the same automorphism coset lead to the same polar subcode, with identical dynamic frozen constraints, but each gives the successive cancellation decoder a different trajectory. So one decoder design can be instantiated $M$ times, run in parallel on $M$ equivalent transformations, and the best candidate kept.

What the paper shows:

- On the (128, 64) extended BCH code, 64 parallel list-4 decoders reach a lower block error rate than one list-512 SCL decoder, with half the effective list size.
- At the same effective list size, 64 members of list size 4 are about 0.5 dB better than 4 members of list size 64. That gap is the diversity the ensemble adds.
- The length does not have to be a power of two. The (24, 12) extended Golay code, decoded through a multi-kernel polar transform, gets close to maximum-likelihood performance with 8 members of list size 2.
- The automorphism group is kept as a base and strong generating set (Schreier–Sims), so drawing $M$ distinct members takes polynomial time.
- Members that differ by an LTA-type (lower-triangular affine) map look the same to a successive cancellation decoder, so they would be wasted. The paper bounds the probability that a uniformly drawn member is redundant in this way, and it is small.

## Early ensemble selection

*2026 to now, paper 2.*

An ensemble of $M$ decoders does roughly $M$ times the work of one. The follow-up question is how early one can tell which members are worth finishing. I am developing early ensemble selection: partway through decoding, the members are scored, either by their path metrics or by a small neural network, and only the most promising ones continue. The aim is to cut the decoding complexity while keeping the block error rate of the full ensemble and its latency advantage.

## Extended BCH codes between two Reed–Muller codes

*2026 to now, paper 3.*

An extended BCH code is sandwiched between two Reed–Muller codes. Labeling its coordinates through a basis of the underlying finite field turns it into a polar-like code, and the choice of basis decides which information set (the pivot profile) the successive cancellation decoder ends up with. I am working out which pivot profiles can be reached through such basis changes, how good the best one can be, and how far the automorphisms of the two code families shrink the search.

## Also on my desk

- Choosing the permutation in the first place: which polar information sets a given code can reach by permuting its coordinates, and how to find a good one.
- Carrying PED over to enhanced polar transformations (arbitrary code lengths) and to non-binary codes, which is the future work listed in paper 1.
- The code equivalence problem and its role in code-based cryptography. For now this is reading.

---

## Earlier

### Robust beamforming

*Summer 2025, visiting student with [Prof. Zhi Ding](https://faculty.engineering.ucdavis.edu/ding/) at UC Davis.*

A convex-optimization-based robust beamforming design for MISO systems under interference and jamming with imperfect channel state information. Against a non-robust baseline it saves 0.5 dB of SNR at a fixed average sum rate. [[code]](https://github.com/eirinnnnnn/robust_miso_doubleQT)
