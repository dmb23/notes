# set up a new repo

Let's say I want to enjoy the combined advantages of Kedro, MLflow, Tensorflow and my own packages.
What I would do to set up an according project is:

```
conda create -n TF_kedro python=3.8 tensorflow-gpu=2.4
conda activate TF_kedro
pip install kedro==0.17.2
kedro new 
kedro install
```

and the things to keep in mind (state 2021/04/28) are:
- I use conda to set up the GPU libraries, then overwrite all python packages by Pip (and use this to organise the dependencies)
- fix `kedro==0.17.2` since 0.17.3 breaks `kedro-mlflow`
- update the Kedro default requirements according to [these improved versions](https://github.com/quantumblacklabs/kedro/issues/735)
    - there is a warning constantly popping up in Jupyter about `should_run_async`, but at least Jedi does not crash
- include my requirements in the respective file

---

## disappearing problems

I already had an issue in Kedro==0.17.2 that `kedro jupyter` or `kedro ipython` was not properly initialized. 
For this I had to adjust `project_root/.ipython/profile_default/startup/00_kedro_init.py` to include the proper path in `sys.path`.
But somehow this is currently not anymore a problem?
