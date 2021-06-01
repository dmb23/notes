# GoTo choice of smoothing

I had to compare my noisy data against a product that was smoothed by the LOESS
implementation in R. My take-home messages are:

- The speed of Savitzky-Golay is beautiful!
- Multiple passes with a smaller window preserve the shape of the original data
  (better than e.g. a single pass with a big window)
- The **position of peaks** in a derivative may **shift** with different
  choices of **window length**!
- I have the feeling that it does not make a difference if you first take the
  derivative and then do multiple smoothing iterations or first smooth and then
  take the derivative. But I did not check the math (or extensive tests)

So if in doubt, I will use 2-5 passes of an Savitzky-Golay filter with
quadratic polynomials.
