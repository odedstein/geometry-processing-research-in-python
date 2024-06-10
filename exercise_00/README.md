# Exercise 00
_Geometry Processing Research in Python_

## Setting up a Python environment

Since this is a Python tutorial, we will start by setting up a Python
environment.

Python's great advantage is its extreme ease of use, but if you're not careful,
then the many different versions of Python and its packages installed in your
environment can quickly become a big mess.
Because of this, I like to set up a new Python virtual environment for each
project of mine.
There are multiple ways to do this -- the two most popular ones are
probably [venv](https://docs.python.org/3/library/venv.html) and
[conda](https://docs.anaconda.com/free/miniconda/).
For the purposes of this tutorial, we will be using venv.
If you prefer to use conda, everything here should work exactly the same as
long as you install the same packages with the same versions.

### venv

venv comes built-in with modern versions of Python.
If you have Python 3.10 or higher (the version supported by this tutorial)
installed, you already have venv.
If you do not have Python installed on your machine, go install the newest
version of Python now.
[The official Python website](https://www.python.org/downloads/) features
detailed installation instuctions.

If you already have Python installed, then
- open your command line;
- navigate to the root directory of this tutorial;
- and create a new venv by issuing the following command (your Python executable might have a different name, such as `python`, `python3` or `python3.10`):
```console
python3 -m venv gp
```

Once your venv is created, you can activate it with
```console
source gp/bin/activate
```
on Mac/Linux, or
```console
gp\Scripts\activate
```
on Windows.

![Creating a new Python venv](images/create_venv.png)
_This is what creating and activating a new Python venv looks like on my Mac._


### Installing packages

In this tutorial, we will use the packages
[_Gpytoolbox_](https://gpytoolbox.org),
[_Polyscope_](https://polyscope.run/py/), [_NumPy_](https://numpy.org),
and [_SciPy_](https://scipy.org).

You can install them into your venv using the console command
```console
python -m pip install numpy==1.26.4 scipy==1.13.1 gpytoolbox==0.2.0 polyscope==2.2.1
```

### Starting Python

Let's now start Python to see whether all packages installed correctly.

You can either save your Python commands in a file `myfile.py` and then
run it with
```console
python myfile.py
```
or you can boot up python in interactive mode with
```console
python
```
and issue all commands line-by-line (end your session with `quit()` or CTRL+D).
*If you follow along this tutorial and want to use interactive mode, please
quit Python and enter a fresh Python session before pasting in a new set of
commands.*

Personally, if I have to run fewer than 3 commands, I will go into interactive
mode, otherwise I find it easier to just have a working script `script.py`
that I repeatedly call with `python script.py`.

So, whether in interactive mode or in your own file, import all our installed
packages and try to run a few basic commands:
```python
import gpytoolbox as gpy
print(gpy.__version__)
import polyscope as ps
print(ps.np.__version__)
import numpy as np
print(np.__version__)
import scipy as sp
print(sp.__version__)
```

You should be seeing the output:
```
0.2.0
1.26.4
1.26.4
1.13.1
```

If this is what you get, then congratulations!
All packages have been installed correctly.
You can continue on to the first real exercise, [exercise_01](../exercise_01).

---

_Oded Stein 2024. [Geometry Processing Research in Python](https://github.com/odedstein/geometry-processing-research-in-python)_

