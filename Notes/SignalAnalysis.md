# Signal Analysis

## Trigonometric Fourier Series
We will utilise and build upon the Trigonometric Fourier Series in this course, thus a quick refresher is provided here. The Fourier Series can be used to decompose period continuous-time signals into sums of sinusoids and co-sinusoids. This helps analyse complex linear systems as sinusoids and co-sinusoids are particular solutions to ordinary differential equations (ODEs).

Any finite power periodic signal $x(t)$ with period $T$ seconds can be represented as a sum of sine and cosines:

$$x(t) = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} A_{n} \cos(n \omega_{0} t) + B_{n} \sin(n \omega_{0} t)$$

Where:

$$f_{0} = \frac{1}{T} \text{Hz} \qquad \omega_{0} = \frac{2 \pi}{T} \text{rad/s}$$

The coefficients $A_{n}$ and $B_{n}$ can be calculated using:

$$A_{n} = \frac{2}{T} \int_{\tau} x(t) \cos(n \omega_{0} t) dt \quad n \in \mathbb{Z}_{0}^{+}$$

$$B_{n} = \frac{2}{T} \int_{\tau} x(t) \sin(n \omega_{0} t) dt \quad n \in \mathbb{Z}^{+}$$

Here $\tau$ is any period of the signal.

### Truncated Fourier Serier Error
The truncated fourier series $\tilde{x}(t)$ using the first $N$ harmonics is:

$$\tilde{x}(t) = \frac{A_{0}}{2} + \sum_{n=1}^{N} A_{n} \cos(n \omega_{0} t) + B_{n} \sin(n \omega_{0} t)$$

The error between this and the original signal is:

$$e_{x,N}(t) = \tilde{x}_{N}(t) - x(t)$$

The size of this error can be measured using the power of a periodic signal:

$$P_{x,N} = \frac{1}{T} \int_{T} | e_{x,N}(t) |^2 dt $$

Clearly, the average error $P_{x,N}$ decreases with increasing number of components N. The error drops by 90\% using just 15 components.

## Determining Fundamental Frequency
As a result of the Fourier Series, we know that periodic signals can be represented as a sum of sinusoids with fundamental frequency $\omega_{0} = \frac{2\pi}{T}$, where T is the fundamental period, and the harmonics have frequency with integer multiples of the fundamental.

Example:

Take the signal:

$$x(t) = 2 + 7 \cos \left(\frac{1}{2}t + \phi_{1} \right) + 3 \cos \left(\frac{2}{3} t + \phi_{2} \right) + 5 \cos \left(\frac{7}{6} t + \phi_{3} \right)$$

The component frequencies are thus:

$$\omega_{1} = \frac{1}{2} \qquad \omega_{2} = \frac{2}{3} \qquad \omega_{3} = \frac{7}{6}$$

As these must be integer multiples of the fundamental for a periodic signal:

$$\frac{\omega_{2}}{\omega_{1}} = \frac{4}{3} = \frac{n_{2} \omega_{0}}{n_{1} \omega_{0}} \implies 4n_{1} = 3n_{2}$$

The lowest positive integers that satisfy this relationship are:

$$n_{1} = 3 \qquad n_{2} = 4$$

Verifying for $\omega_{3}$:

$$\frac{\omega_{3}}{\omega_{2}} = \frac{7}{4} = \frac{n_{3} \omega_{0}}{n_{2} \omega_{0}} \implies n_{3} = \frac{7}{4}n_{2} \implies n_{3} = 7$$

The signal $x(t)$ is periodic, with fundamental frequency $\omega_{0} = \frac{\omega_{1}}{n_{1}} = \frac{1}{6}$ , and contains the 3rd, 4th and 7th harmonics.

## Complex Phasors
A phasor is a complex signal, that has both a real and imaginary component, and is able to relay information about amplitude, frequency and phase. 

The complex phasor is generally stated as per Euler's formula:

$$A\cos(\omega_{0}t) + jA \sin(\omega_{0} t) = A \exp(j\omega_{0} t) = Ae^{j\omega_{0} t}$$

As $\cos$ is an even function, and $\sin$ is odd:

$$Ae^{-j\omega_{0} t} = A \cos(\omega_{0} t) - j \sin(\omega_{0} t)$$

Therefore:

$$\cos(\omega_{0} t) = \frac{e^{j\omega_{0}t} + e^{-j\omega_{0}t}}{2}$$

$$\sin(\omega_{0} t) = \frac{e^{j\omega_{0}t} - e^{-j\omega_{0}t}}{2j}$$

## Deriving Complex Fourier Series
We begin with the general form for the trigonometric fourier series:

$$x(t) = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} A_{n} \cos(n \omega_{0} t) + B_{n} \sin(n \omega_{0} t)$$


We substitute the [complex relationships for sin and cos](#complex-phasors):

$$x(t) = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} \left[A_{n} \left(\frac{e^{jn\omega_{0}t} + e^{-jn\omega_{0}t}}{2} \right) + B_{n} \left(\frac{e^{jn\omega_{0}t} - e^{-jn\omega_{0}t}}{2j} \right)\right]$$

Grouping terms:

$$x(t) = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} \left[A_{n}\frac{e^{jn\omega_{0}t}}{2} + A_{n}\frac{e^{-jn\omega_{0}t}}{2} + B_{n} \frac{e^{jn\omega_{0}t}}{2j} - B_{n} \frac{e^{-jn\omega_{0}t}}{2j} \right]$$

$$= \frac{A_{0}}{2} + \sum_{n=1}^{\infty} \left[A_{n}\frac{e^{jn\omega_{0}t}}{2} + A_{n}\frac{e^{-jn\omega_{0}t}}{2} - B_{n} \frac{je^{jn\omega_{0}t}}{2} + B_{n} \frac{je^{-jn\omega_{0}t}}{2} \right]$$

$$ = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} \left[\left(\frac{A_{n} - jB_{n}}{2} \right) e^{jn\omega_{0}t} \right] + \sum_{n=1}^{\infty} \left[\left(\frac{A_{n} + jB_{n}}{2} \right)e^{-jn\omega_{0}t} \right]$$

Changing the bounds of the second summation using the substitution $m=-n$:
$$x(t) = \frac{A_{0}}{2} + \sum_{n=1}^{\infty} \left[\left(\frac{A_{n} - jB_{n}}{2} \right) e^{jn\omega_{0}t} \right] + \sum_{m=-\infty}^{-1} \left[\left(\frac{A_{-m} + jB_{-m}}{2} \right)e^{jn\omega_{0}t} \right]$$

Defining the complex fourier coefficient as:
```math
X_{n} =
\begin{cases}
    \frac{A_{n} - jB_{n}}{2}, & \text{if $n > 0$}\\
    \frac{A_{0}}{2}, & \text{if n = 0}\\
    \frac{A_{-n} + jB_{-n}}{2}, & \text{if n < 0}
\end{cases}
```

>**Note:** $X_{n}$ is conjugate symmetric, i.e. $X_{-n} = X_{n}^{\ast}$. This means, $|X_{-n}| = |X_{n}|$, so the magnitude is even, and $\angle X_{-n} = - \angle X_{n}$, so the phase is even
 
As the summations cover all integers $n \in (-\infty, \infty)$ the equation can be simplified to:

$$x(t) = \sum_{n=-\infty}^{\infty} X_{n} e^{jn\omega_{0}t}$$

### Relationship between Complex and Trigonometric Coefficients
Observing the integral definitions for calculating $A_{n}$ and $B_{n}$ clearly:

$$A_{-n} = A_{n} \qquad B_{-n} = -B_{n} \qquad B_{0} = 0$$

Thus, we define the complex fourier coefficient simply as:

$$X_{n} = \frac{A_{n} - jB_{n}}{2}$$

### Calculating Complex Fourier Coefficient
There are multiple ways to derive the Complex Fourier Coefficient. The simplest I have found is as follows. We have now found the general relationship between the [complex and trigonometric Fourier coefficients](#relationship-between-complex-and-trigonometric-coefficients), we thus substitute the equations for the trigonometric coefficients:

$$X_{n} = \frac{A_{n} - jB_{n}}{2} = \frac{\frac{2}{T}\int_{\tau} x(t) \cos(n\omega_{0} t) dt -j \frac{2}{T}\int_{\tau} x(t) \sin(n\omega_{0} t) dt}{2}$$

Simplifying:
$$= \frac{1}{T} \int_{\tau} x(t) (cos(n\omega_{0} t) - j \sin(n\omega_{0}t))dt$$

$$\implies X_{n} = \frac{1}{T} \int_{\tau} x(t) e^{-jn\omega_{0}t}dt$$
