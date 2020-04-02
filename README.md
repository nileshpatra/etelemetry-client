## Etelemetry-client

[![Build Status](https://travis-ci.org/sensein/etelemetry-client.svg?branch=master)](https://travis-ci.org/sensein/etelemetry-client)
[![codecov](https://codecov.io/gh/sensein/etelemetry-client/branch/master/graph/badge.svg)](https://codecov.io/gh/sensein/etelemetry-client)

A lightweight python client to communicate with the etelemetry server

### Installation

```
pip install etelemetry
```

### Usage

```python
import etelemetry
etelemetry.get_project("nipy/nipype")

{'version': '1.4.2', 'bad_versions': ['1.2.1', '1.2.3', '1.3.0']}
```

or to take advantage of comparing and checking for bad versions, you
can use the following form

```python
import etelemetry
etelemetry.check_available_version("nipy/nipype", "1.2.1")

A newer version (1.4.2) of nipy/nipype is available. You are using 1.2.1
You are using a version of nipy/nipype with a critical bug. Please use a different version.
returns: {'version': '1.4.2', 'bad_versions': ['1.2.1', '1.2.3', '1.3.0']}
```

### Adding etelemetry to your project

You can include etelemetry in your project by adding `etelemetry` package to your setup process 
and by adding the following snippet to your `__init__.py`. The code snippet below assumes you 
have a `__version__` and `usemylogger` (logger) variables available.

```python
# Run telemetry on import for interactive sessions, such as IPython, Jupyter
# notebooks, Python REPL
import __main__

if not hasattr(__main__, "__file__"):
    import etelemetry
    etelemetry.check_available_version("dandi/dandi-cli", __version__, lgr=usemylogger)
```

To add support checking for bad versions you will need to add a file named
`.et` to your github project containing a simple json snippet. 

```json
{ "bad_versions" : []
}
```

Here is an example: https://github.com/nipy/nipype/blob/master/.et
