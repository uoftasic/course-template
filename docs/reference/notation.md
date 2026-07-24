# Notation

Common symbols for UofT ASIC course notes. Extend per course.

| Symbol | Meaning |
|--------|---------|
| $t$ | Time |
| $f_s$ | Sampling frequency |
| $V_{DD}$ | Supply voltage |
| $\mathbf{x}$ | Column vector |
| $\mathbf{X}$ | Matrix |
| $\mathbb{E}[\cdot]$ | Expectation |
| $\|\mathbf{x}\|_2$ | Euclidean norm |

## Example identities

Fourier transform (continuous):

$$
X(f) = \int_{-\infty}^{\infty} x(t)\, e^{-j 2\pi f t}\, dt
$$

Parseval (energy):

$$
\int_{-\infty}^{\infty} |x(t)|^2\, dt = \int_{-\infty}^{\infty} |X(f)|^2\, df
$$
