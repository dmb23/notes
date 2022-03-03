# Fast (?) python environment on Mac M1

what did I find so far on the big question: how to get an efficient python setup?

1. set up an `mambaforge` environment
    - *mambaforge* is supposed to be better with ARM than conda 
1. required packages:
    - `python`
    - `cython`, `pybind11` to compile numpy later
    - `apple::tensorflow-deps`
    - plus the required other packages like Jupyter, Pandas, matplotlib, ...
1. compile numpy using Apples VecLib as BLAS interface:
    - `pip install --no-binary :all: --no-use-pep517 --force-reinstall numpy`
    - this is based on a comment that I can't link directly made by user [graphitump](https://developer.apple.com/forums/thread/695963) in the [Apple Developer Forums](https://developer.apple.com/forums/thread/695963)
1. install tensorflow with the metal plugin:
    - `pip install tensorflow-macos`
    - `pip install tensorflow-metal`

This sequence allowed me to have everything running in the end. I did not yet test extensively, let's hope it works... Also: so far I don't see a clean way of automating this.
