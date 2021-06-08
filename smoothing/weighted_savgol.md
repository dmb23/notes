# Weighted Savitzky-Golay

Savitzky-Golay filtering is **fast**, since it relies on equally spaced *x* values to
pre-calculate some global constants and then smooth just by a convolution. Even though it 
is not often pre-implemented, it should be easily possible to adjust this process with 
(common) weights. For example LOESS proposes to use a tri-cubic weighting function to weight
the role of a variable in the regression according to its distance from the target point. This is mostly done 
to account for unevenly spaced samples, but could also be interesting otherwise, maybe?

[This extremely surprising source](https://en.wikipedia.org/wiki/Weighted_least_squares) in 
combination with this [beautiful implementation](https://github.com/scipy/scipy/blob/v1.6.3/scipy/signal/_savitzky_golay.py#L8-L139)
offer a way how to do this:

## Basic implementation

the key steps in SciPy are:

-  create the vector of positional offsets
    - `halflen = window_length // 2`
-  reverse its order, so it can be used with a convolution
    - `z = np.arange(-halflen, window_length - halflen, dtype=float)`
    - `z = [::-1]`
-  create the system matrix (partial Vandermonde Matrix)
    - `order = np.arange(poly_order + 1).reshape(-1, 1)`
    - `A = z ** order`
- create the target Vector for the linear set of equations: zero out all derivatives we are not interested in, then include scaling values to account for *delta* and the degree of the derivative
    - `scale_vals = np.zeros(polyorder + 1)`
    `scale_vals[deriv] = float_factorial(deriv) / (delta ** deriv)`
- finally create the pseudoinverse $(A^TA)^{-1}A$, which will contain the coefficients for the smoothing, as a solution to a least squares problem
    - `coeffs, _, _, _ = lstsq(A, scale_vals)`
- those can then be convolved with the signal that should be smoothed
    - `y = convolve1d(x, coeffs, axis=axis, mode='constant')`
    - and do something about the edges...

## Update to include weights

Apparently, the normal equation for the weighted coefficients would be $(A^TWA)c = A^TWy$ (for a diagonal weight matrix $W$).
This can be simplified by defining

- $X' = \diag(w)X$
- $y' = \diag(w)y$

and then solving directly $(X'^TX') c = X'^T y'$. This means for the implementation:
- scale the system matrix `A` 
- figure out which target vector to scale - I think it should be `y`?
- in the article they derive the original weights as $W_{ii} = 1 / \sigma_{I}^2$, and use $w_i = \sqrt{W_{ii}}$ for the effective scaling. I.e. when calculating the weights, do I need to take the square root?

Many open questions, but should be possible if needed!
