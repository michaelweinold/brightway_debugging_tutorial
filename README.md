# Brightway Debugging in VS Code

## VS Code Setup

`launch.json`:

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        
        {
            "name": "Python Brightway Debugger",
            "type": "debugpy",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "python": "${workspaceFolder}/.myvenv/bin/python",
            "justMyCode": false,
            "stopOnEntry": false,
            "env": {"PYTEST_ADDOPTS": "--no-cov"},
            "purpose": [
                "debug-test"
            ],
            "console": "integratedTerminal",
        }
    ]
}
```

Creat the virtual environment using:

```
pip install brightway25 ipykernel
```

This will install the packages of the [Brightway framework for sustainability assessment](https://docs.brightway.dev/en/latest/). It is likely that the issue lies with these packages.

## Working Example

```
.
├── .myvenv
├── data.csv
└── myfile.py
```

`myfile.py`:

```python
# %%
import pandas as pd
df = pd.read_csv('data.csv') #🔴
```

If I use the VS Code Python debugger, this work as expected:

The file is run, but execution stops at the line with the breakpoint (`#🔴`). I can then choose to step into the function call and follow its logic in the Pandas package source code.

## How can I get this to work?

```
.
├── .myvenv
└── myfile.py
```

`myfile.py`:

```python
# %%
import bw2data as bd
bd.projects.report() #🔴
bd.projects.set_current(name="test") #🔴
```

Execution stops at _neither_ breakpoint. Why? This must be package-specific?

