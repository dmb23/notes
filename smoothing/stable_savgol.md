# stable Savitzky-Golay

One advantage of LOESS is that it is quite stable against outliers: It iterates multiple times over the residual to the fit.
Each residuum is compared against the median residuum *s*: any residuum *r* is normalized to *x = r/(6s)*, and then weighted by an bi-square weight function 
![\begin{align*}
B(x) = \begin{cases}
(1 - | x |^2)^2 &\text{for} \;|x| < 1\\
0 &\text{for}\; |x|\geq 1
\end{cases}
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0AB%28x%29+%3D+%5Cbegin%7Bcases%7D%0A%281+-+%7C+x+%7C%5E2%29%5E2+%26%5Ctext%7Bfor%7D+%5C%3B%7Cx%7C+%3C+1%5C%5C%0A0+%26%5Ctext%7Bfor%7D%5C%3B+%7Cx%7C%5Cgeq+1%0A%5Cend%7Bcases%7D%0A%5Cend%7Balign%2A%7D%0A)
In a new iteration the weights of the weighted least squares are then adjusted by the factor *B*. 

What is bad about LOESS: this is expensive! What is nice about Savitzky-Golay: it is fast - but it can't include data-dependent weights, or it loses its advantage of convolving uniform weights.
So lets just change the approximation data iteratively: 

- Do a first round of Savitzky-Golay
- calculate interpolated points and residuuals
- do a weighted linear interpolation between original data and interpolation values, so use the residuum-based weights to change the data points
- and then iterate.

This should have a similar effect, but be much more fast. (disclaimer: this has not been tried yet...)
