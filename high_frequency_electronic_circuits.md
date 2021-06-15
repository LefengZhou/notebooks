# Electronic Circuits

the figures and examples are from _RF Microelectronics, Second Edition_ written by Behzad Razavi. read these notes with the figures.

## Basic Concepts in RF Design

### Time Variance

* time variance generates new frequency components.
* an ideal mixer (figure 2.2) is time variant. whether it is nonlinear depends on which port is modeled as input of the system.

### Nonlinearity

single tone test:
$$
y(t) = a_0 + a_1 x(t) + a_2 x^2(t) + a_3 x^3(t) \\
x(t) = A\cos \omega t\\
y(t) = \frac{1}{2}a_2 A^2 + (a_1 A +\frac{3}{4}a_3 A^3 )\cos \omega t + \frac{1}{2}a_2 A^2\cos 2\omega t +\frac{1}{4}a_3 A^3 \cos 3\omega t
$$
two tone test:
$$
x(t) = A_1\cos\omega_1 t + A_2\cos\omega_2 t
$$
nonlinear effect:

* harmonics (one signal input)
* gain compression (one signal input)
  * self-desensitization
  * condition: $ a_1 a_3 < 0 $
  * 1-dB compression point: $20\lg (a_1 A +\frac{3}{4}a_3 A^3) = 20\lg (a_1 A) -1 \Longrightarrow A_{in,1dB} = \sqrt{0.145|a_1/a_3|}$
* desensitization (small signal + large interferer)
  * energy transfer between frequency components
  * component of  $\omega_s+\omega_i-\omega_i$ compresses $\omega_s$ .
  * $y_{fund}(t) = (a_1+\frac{3}{2}a_3A_i^2)A_s\cos \omega_s t$
* cross modulation (signal + AM interferer)
  * information transfer between frequency components
  * AM of the interferer is modulated on the signal.
  * $y_{fund}(t) = (a_1+\frac{3}{2}a_3A_i^2(t))A_s\cos \omega_s t$
  * constant-envelope mod schemes do not suffer from cross modulation.
* intermodulation (two interferers)
  * component of $\omega_{i1} + \omega_{i1} - \omega_{i2} = \omega_s$ interferes $\omega_s$ .
  * $y_{i}(t) = \frac{3}{4}a_3A_{i1}^2A_{i2}\cos(2\omega_{i1}-\omega_{i2})t$
  * IP3: $a_1A_s = \frac{3}{4}a_3A_{i1}^2A_{i2}$ , assume that $A_s = A_{i1} = A_{i2} = A$
  * input IP3 $A_{IIP3} = \sqrt{1.33|a_1/a_3|}$ , 9.6 dB higher than 1-dB compression point
  * IP3 requirement can be calculated without any assumption on input impedance. (example 2.11, the solution is wrong)
* spectral regrowth (signals at nonlinear PA)
  * self-intermodulation of variable-envelope signals

cascade nonlinear stages
$$
\frac{1}{A^2_{IP3}} \approx \frac{1}{A^2_{IP3,1}}+\frac{a_1^2}{A^2_{IP3,2}}+\frac{a_1^2 b_1^2}{A^2_{IP3,3}} + \cdots
$$
the gains of front stages make the nonlinearity of back stages more significant.

### Noise

* thermal noise of resistors $S_V(f) = \bar{V_n^2} = 4kTR$

* effect of transfer function on noise $S_o(f) = S_i(f)|H(f)|^2$

* noise figure (figure 2.48)
  $$
  NF = \frac{SNR_{in}}{SNR_{out}} = 1 + \frac{\bar{V_{n,o}^2}}{\bar{V_{n,RS}}|\alpha|^2 A^2} = 1 + \frac{\bar{V_{n,i}^2}}{\bar{V_{n,RS}}}
  $$

* cascade noisy stages
  $$
  NF = 1 + (NF_1-1) + \frac{NF_2-1}{A_{P1}} +  \frac{NF_3-1}{A_{P1}A_{P2}} + \cdots , A_P = \frac{P_{out,av}}{P_{in,av}}
  $$

* the gain from front stages make the noise of back stages insignificant.

### Sensitivity

$$
NF = \frac{SNR_{in}}{SNR_{out}} = \frac{P_{sig}/P_{RS}}{SNR_{out}} \\
P_{sig} = SNR_{out}\cdot P_{RS}\cdot NF \\
P_{sig,tot} = SNR_{out}\cdot P_{RS}\cdot NF\cdot BW
$$

### Passive Impedance Transformation

* L-match
  * RC transformation (figure 2.58)
    * $Q_s = (1/C_s\omega)/R_s, Q_p = R_p/(1/C_p\omega) $ , Q = storage/loss
    * $Q_s = Q_p = Q$ , see the circuits as non-ideal capacitors, so Q must remain the same.
    * if $Q \gg 1$ , the circuits behave as capacitors (consider the extreme case of ideal capacitors) so that the transformation do not change capacitance, $C_s \approx C_p$ .
    * transformation of resistance: $Q^2 = Q_s Q_p = R_p/R_s$
    * there exists an accurate derivation without the condition of high Q.
  * RL transformation: derivation of RL transformation is the same as RC.
  * L-match has 2 degrees of freedom: transformation ratio and resonance frequency completely determine L and C.
* Pi-match and T-match
  * combinations of L-match: transform the impedance up, and down
  * more than 2 degrees of freedom
* transformer (figure 2.64)

## Communication Concepts

* AM
  * highly linear PA required
  * sensitive to additive noise
* PM
  * $x_{FM}(t) = A_c \cos(\omega_c t + m\int A_m\cos\omega_m t dt)$
  * under narrowband FM approximation $mA_m/\omega_m \ll 1$ , there are sidebands at $\omega_c\pm\omega_m$ .
* digital modulation

## Transceiver Architectures

###  Heterodyne Receiver Architecture

* antenna ---- band-selection filter ---- LNA ---- image-reject filter ---- mixer ---- channel-selection filter ----
  * band-selection filter
    * do not perform channel selection here because it is impossible that a filter has such a high Q at the same time the central frequency is adjustable.
    * trade off: in-band loss (noise) and out-of-band attenuation
  * image-reject filter
    * small attenuation in the desired band, large attenuation in the image band at $2\omega_{LO}-\omega_{RF}$
  * mixer
    * trade off: high IF leads to difficult channel selection, and low IF leads to difficult image rejection
    * solution: dual down-conversion
* ---- LNA ---- image-reject filter 1 ---- RF mixer ---- partial-channel-selection filter ---- amp ---- IF mixer ---- channel-selection filter ---- (figure 4.16)
  * dual down-conversion: high IF1 (easier image rejection) and progressive channel selection
  * problem: (1) secondary image of IF mixer; (2) mixing spurs; (3) oscillators coupling 
  * solution: 
    * zero second IF, with quadrature down-conversion to avoid self-image (figure 4.24)
    * sliding IF: one oscillator to drive all mixers.

### Homodyne Receiver Architecture

* advantages to heterodyne architecture
  * no image (quadrature down-conversion to avoid self-image)
  * channel selection is performed by LPF
  * less mixing spurs
* problems
  * LO-RF feedthrough
    * solution: symmetric layout and differential output
  * RF-LO feedthrough: injection pulling

### Direct-Conversion Transmitter Architecture

problems

* IQ mismatch
  * $x(t) = a_1(A+dA)\cos(\omega t+d\theta) - a_2A\sin\omega t$
* carrier leakage
  * $x(t) = (a_1A+V_1)\cos\omega t - (a_2A+V_2)\sin \omega t$
  * solution: generate $a_1 = a_2 = 0$ and detect the leakage, then compensate it.
* injection pulling
  * solution: (1) frequency divider, which also provides quadrature carriers. but it will be pulled by the second harmonics of RF signals. (2) frequency doubler

## Low-Noise Amplifiers

### General Considerations

* requirement of low noise figure: 2~3 dB
* gain
  * large enough to minimize the noise contributions of subsequent stages (mixers)
  * tradeoff: large gain leads to pronounced nonlinearity of subsequent stages.
* input matching
  * where?
    * antenna ---- (off-chip filter) ---- LNA
  * why?
    * the standard termination of off-chip filters
    * loss of the antenna if unmatched: the antenna is designed for real load impedance.
    * input return loss: long distance between the antenna and LNA causes reflection.
* other considerations
  * bandwidth: flat response required
    * preferably less than 1 dB of gain variation in frequency range of interest
  * power dissipation
    * not as critical as noise in LNA design

### LNA Topologies

target: input matching of 50 Ohm without the noise of a 50-Ohm resistor. a passive matching network is impossible (example 5.5)

* CS stage with resistive feedback (figure 5.13)
* inductive-degenerate LNA (figure 5.31)

## Mixers

### General Considerations

* mixing spurs
  * cause: harmonic components of square wave
  * dealt with at architecture level. solutions:
    * no more than 2 down-conversion steps
    * choosing LO frequency carefully
    * homodyne architecture
* port-to-port feedthrough
  * cause: device capacitance (example 6.1)
  * the key problem: under what scenarios will the feedthrough become harmful? 
    * answer: under the scenarios that **the interferer and the signal have similar frequency**.
  * | feedthrough | homodyne                                                     | heterodyne                                                   |
    | ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | LO-RF       | DC offsets in baseband (example 6.1, self mixing of homodyne RX); the antenna of TX emits large interferer from LO |                                                              |
    | RF-LO       | injection pulling                                            |                                                              |
    | LO-IF       |                                                              | LO desensitizes the following stages if IF and LO frequency are close, otherwise it is suppressed by filters |
    | IF-LO       |                                                              | injection pulling if IF and LO frequency are close           |
    | IF-RF       |                                                              |                                                              |
    | RF-IF       | beat component in the RF path corrupt baseband               |                                                              |
  * solution of injection pulling: a buffer between the LO and the mixer
* noise
  * SSB NF = 3 dB. for a noiseless heterodyne RX, the noise from the image band will add to the signal band. SSB means that the signal band is at one side of IF.
  * DSB NF = 0 dB. homodyne RX does not encounter the problems of image band.
* the troubles of LO waveforms
  * square wave (ideal)
    * mixing spur
    * abrupt switching cannot be achieved at very high frequency. LO waveform approximates to sinusoids.
  * sinusoidal wave (at very high frequency)
    * gain reduction, especially in balanced topologies with differential outputs. (figure 6.17)
    * solution of gain reduction: large amplitude to reduce the time of transition.

### Mixer Topologies

* the problem of single-ended mixers (figure 6.3):
  * discard half of signals. gain = 1/pi = -10 dB
  * for all RZ (return-to-zero) mixers, the square wave produced by the switch contains DC component. so the beat (2nd-order NL) of RF signals still exists in the baseband. so it is ill-suited to direct conversion RX.
* single-balanced mixers (figure 6.15): balanced LO waveform
  * advantages
    * twice the gain than singled-ended mixers. gain = 2/pi = -4 dB
    * natural differential outputs
    * symmetric circuit canceling the LO-RF feedthrough (DC offsets)
  * problems
    * doubled LO-IF feedthrough
* double-balanced mixers (figure 6.16): balanced LO waveform and balanced RF input
  * advantages: cancel LO-IF feedthrough
  * problems:
    * the gain is the same as single-balanced mixers. gain = 2/pi = -4 dB
* sampling mixers (figure 6.21):
  * advantages:
    * for a single-ended sampling mixer, gain = sqrt(1/pi^2+1/4) = -4.54 dB
    * we can apply single-balanced topology to sampling mixers, acquiring doubled gain. despite of passive circuits, the gain is greater than unity! gain = 1.48 dB
  * problems:
    * caution that the gain of double-balanced topology is still -4 dB, because the gain of sampling mixers results from the capacitors holding the voltage while the switch of the port is open. but in double-balanced topology, there are 2 switches connected to 1 port, which are never open simultaneously. (example 6.8) solution: double-balanced sampling mixers in current domain (figure 6.26)
* active down conversion mixers:
  * 3 functions (figure 6.41): RF voltage $\longrightarrow$ RF current  $\xrightarrow[]{\mathrm{LO}}$ IF current $\longrightarrow$ IF voltage
  * single-balanced topology (figure 6.42)
    * correspond to 3 functions, $\mathrm{gain} = A_{V/I}A_{LO}A_{I/V} = g_{m1}\cdot \frac{2}{\pi} \cdot R_D$
    * note that the 1st harmonic of the switch function swinging from -1 to 1 is 4/pi.
  * double-balanced topology (figure 6.43)
    * advantages: reject amplitude noise in the LO waveform

## Oscillators

### General Principles

#### Feedback View of Oscillators

* view: a feedback system
* Barkhausen's criteria for **sustained** oscillation (figure 8.8):
  * negative feedback system: 180 degree feedback phase shift
  * 180 degree frequency-dependent phase shift $\angle H(j\omega_1) = \pi$ (360 degree total phase shift)
  * unity gain $|H(j\omega_1)| = 1$
* in fact, a system satisfying the criteria above is a positive feedback system with loop gain $\beta(j\omega_1) A = 1$ , where $\beta(j\omega)$ is the feedback and $A$ is the amplification. [Barkhausen's criteria](https://en.wikipedia.org/wiki/Barkhausen_stability_criterion)

#### One-Port View of Oscillators

* view: a lossy resonator + a negative resistance to cancel the loss (figure 8.13)

### Oscillator Topologies

* cross-coupled oscillator
  * each of the 2 stages provides gain $g_m R_p$ and 180 degree phase shift at the resonance frequency. (figure 8.17)
  * a more robust circuit (figure 8.18b, example 8.11)
* ring oscillator (figure 8.11)
  * 3 CMOS inverters
  * output the frequency component who experiences a total 360 degree phase shift.
* three-point oscillator
  * criteria of oscillation
    * parallel resonance (0 resistance)
    * $X_{cb}+X_{be}+X_{ce} = 0,X_{be}X_{ce}>0$
    * [射同基反](https://www.doc88.com/p-698300338712.html)
* quartz oscillator
  * effective circuit of quartz crystals
  * usage: as inductor or as short circuit
* VCO (figure 8.25)
  * key component: varactor

## Power Amplifiers

### General Consideration

* starting point 1: reduce the voltage experienced by the transistor (figure 12.1)
  * a big L to offer DC current only and a big C to pass AC current only (figure 12.1c)
  * voltage of the load swings from 0 to $2V_{DD}$, current of the load from 0 to $2I_{L1}$ .
  * solution: matching network to transform the load resistance to a lower value
* starting point 2: increase efficiency
  * $\eta = P_L/P_{supp}$
  * solution: decrease conduction angle

### PA Classes

trade off: output power, nonlinearity and efficiency

* a uniform topology for 3 classes: frequency selecting amplifier
  * CS stages with a parallel RLC load. (figure 12.1, replace $R_L$ with RLC tank, where LC resonates at $\omega_0$ and R is the load.)
  * LC resonates at fundamental frequency, and passes DC and all other harmonic current. So, only the fundamental harmonics will pass the load R.
  * the difference among 3 classes is the conduction angle.
* class A (figure 12.11)
  * linear, conduction angle = 360 degree
  * $\eta = 0.5$ (figure 12.11)
* class B
  * nonlinear, conduction angle = 180 degree
  * $\eta = \pi/4$
* class C
  * nonlinear, conduction angle < 180 degree
  * $\eta = \frac{1}{4}\frac{\theta - \sin \theta}{\sin(\theta/2) - (\theta/2)\cos(\theta/2)}, P_{out} \propto \frac{\theta-\sin\theta}{1-\cos(\theta/2)}$

## Appendix

### Decibel

sinusoidal signal of 0 dBm delivered to 50 Ohm load $\Longrightarrow$ 632 mVpp, 316 mVp (example 2.1)

### Fourier Series

calculate triangular series to get fundamental harmonics. if $x(t)$ is anti-symmetric,
$$
x(t)= a_0 + a_1\sin\omega_0 t + a_2\sin 2\omega_0 t +\cdots \\
a_1 = \frac{2}{T}\int_0^T x(t)\sin\omega_0 t dt
$$
switch function of ideal mixer: square wave of 50% duty cycle
$$
S(t) = \frac{1}{2} + \frac{2}{\pi}\sin\omega t + \cdots
$$
$S(t)-S(t-T/2)$ swings from -1 to 1,
$$
S(t)-S(t-T/2) = \frac{4}{\pi} \sin\omega t + \cdots
$$

### Resonating Circuits

parallel RLC
$$
Q = \frac{R}{\omega_0 L} = \frac{R}{\frac{1}{\omega_0 C}} = R\sqrt{\frac{C}{L}},\omega_0 = \sqrt{\frac{1}{LC}} \\
\left|\frac{V}{V_{max}}\right| = \frac{1}{\sqrt{1+(Q_p\cdot2\frac{\Delta\omega}{\omega_p})^2}}
$$
