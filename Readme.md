# make_var

- Retrieve all variables defined by make command from **python**
- Expand make type variables `$(VAR)` in string

Package allow you to access any symbol defined in *make*.
It might be helpful to transfer your *Makefile* based project
to different one.

## Installation

`pip install make_var`

## Tutorial

- just create simple Makefile containing
```
H = hello
W = world
```

- create python file `test.py`
```
#!/usr/bin/env python3
from make_var import *

M=make_vars(origin=['makefile']) # retrieve only data defined in makefiles
print(M['makefile']['H'], M['makefile']['W'])
```

you get
`hello world`

- to get all variables that `make` uses just write
```
M=make_vars(origin=None)        # all variables
print(M.keys())                 # print all origins
```
output is
`['environment', "'override'", 'automatic', 'makefile', 'default']`

## Tutorial variable expansion
 - use same Makefile
 - edit python file

```
print(make_expand(M,"$(H) $(W)")) # replaces $(H) with "hello" and $(W) with "word"
```

you get
`hello world`

## Internals

package is based on GNU make command
`make -pnB`
