carbonite
=========

Freeze your Python package dependencies

### Installation ###

`pip install carbonite`

### What's It Do? ###

Carbonite provides a command line tool that acts on a Python module specifying some floating dependencies for your project. It takes these floating dependencies, installs them using Pip to get the current versions, then writes a new Python file that looks like your old one but with static dependencies.

Basically, it takes this:

```python
# file: input.py

# we use a __carbonite__ variable to tell carbonite which vars to operate on
__carbonite__ = ['INSTALL_REQUIRES']

# this has to be a list of strings specifying package versions
INSTALL_REQUIRES = ['requests >= 2.0.0']
```

Resolves and installs those dependencies, then creates a different file that looks like this:

```python
INSTALL_REQUIRES = ['requests==2.3.0']
```

### Usage ###

The command line tool takes the following args:

```
carbonite <path to input file> <path to output file>
```

In our previous example then, we would have said:

```
carbonite input.py output.py
```
