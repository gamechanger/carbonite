carbonite
=========

Freeze your Python package dependencies

### Installation ###

`pip install carbonite`

### What's It Do? ###

Carbonite provides a command line tool that acts on a Python module specifying some floating dependencies for your project. It takes these floating dependencies, installs them using Pip to get the current versions, then writes a new Python file that looks like your old one but with static dependencies.

Basically, it takes a file like this as input:

```python
# we use a __carbonite__ variable to tell carbonite which vars to operate on
__carbonite__ = ['INSTALL_REQUIRES']

# this has to be a list of strings specifying package versions
INSTALL_REQUIRES = ['Flask >= 0.10.1']
```

Carbonite then resolves and installs those dependencies. If that succeeds, it then creates a new Python file that has frozen versions of the packages you specified and their dependencies, all the way down the dependency graph:

```python
INSTALL_REQUIRES = [
    "Flask==0.10.1",
    "itsdangerous==0.24",
    "Jinja2==2.7",
    "Werkzeug==0.9.6",
    "MarkupSafe==0.23",
]
```

### Why not use pip freeze? ###

Carbonite gives you the following advantages over `pip freeze`:

1. `pip freeze` outputs every single package installed in your current Python environment. Carbonite works from a specific list, so you are able to only list the packages specific to your current context.
1. Carbonite allows you to separate dependencies into groups. You can specify your install and test package dependencies separate, saving your users some build time if they don't need to run tests.
1. The output from Carbonite is a valid Python file and can be easily imported for use in `setup.py` scripts.

### Usage ###

The command line tool reads in an input file and writes to a separate output file. Once you've installed, it's as easy as running this:

```
carbonite <path to input file> <path to output file>
```
