# Fast (?) python environment on Mac M1

what did I find so far on the big question: how to get an efficient python setup?

1. set up an `mambaforge` environment, either directly or via pyenv
    - *mambaforge* is supposed to be better with ARM than conda 
1. install minimal required packages for pip:
    - `python==3.8` (3.8 required for `tensorflow-macos`)
    - `cython`, `pybind11` to compile numpy later
    - `apple::tensorflow-deps` as required by the [Apple install instructions](https://developer.apple.com/metal/tensorflow-plugin/)
    - **not more!** When I tried to install more packages at this point, the compilation of Numpy would fail.
1. compile numpy using Apples VecLib as BLAS interface:
    - `pip install --no-binary :all: --no-use-pep517 --force-reinstall numpy==1.21.5`
    - this is based on a comment that I can't link directly made by user [graphitump](https://developer.apple.com/forums/thread/695963) in the [Apple Developer Forums](https://developer.apple.com/forums/thread/695963). Refers to [this stackoverflow answer](https://stackoverflow.com/a/66536896)
    - the version number for Numpy helps that conda does not try to overwrite it by a higher-priority channel later. Might change in the future.
1. install tensorflow with the metal plugin *via Pip*:
    - `pip install tensorflow-macos`
    - `pip install tensorflow-metal`
1. if not already done: tell conda to include pip packages in its requirements resolution
    - `conda config --set pip_interop_enabled True`
1. lastly, install missing packages via conda
    - `conda install pandas jupyter matplotlib cmocean seaborn scipy scikit-learn black isort`

This sequence allowed me to have everything running in the end. I did not yet test extensively, let's hope it works... Also: so far I don't see a clean way of automating this.
