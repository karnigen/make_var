# make_var

- Retrieve all variables defined by make command by **python**
- Expand make type variables `$(VAR)` in string

Package allow you to access any symbol defined in *make*.
It might be helpful to transfer your *Makefile* based project
to different one.

## Installation

`pip install make_var`

## Tutorial

How to use package:

- just create simple Makefile containing variables H and W
```
H = hello
W = world
```

- next create python file `read_makefile.py`
```
#!/usr/bin/env python3
from make_var import *

M=make_vars(origin=['makefile']) # retrieve only data defined in makefiles
print(M['makefile']['H'], M['makefile']['W'])
```

execute it and you get
`hello world`

- to get all variables that `make` uses just write
```
M=make_vars(origin=None)        # all variables
print(M.keys())                 # print all origins
```
output is
`['environment', "'override'", 'automatic', 'makefile', 'default']`

## String expansion
Example to replace $(var) by definition from Makefile
 - use same Makefile as before
 - edit python file

```
print(make_expand(M,"$(H) $(W)")) # replaces $(H) with "hello" and $(W) with "word"
```

you get
`hello world`

## Internals

package is based on GNU make command
`make -pnB`
