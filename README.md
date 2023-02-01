# lbpytest

[![PyPI](https://img.shields.io/pypi/v/lbpytest)](https://pypi.org/project/lbpytest/)

Utilities for Python-driven integration tests at LINBIT.

## Installation

```bash
pip install lbpytest
```

## Usage

### [ControlMaster](./src/lbpytest/controlmaster.py)

```python
from lbpytest.controlmaster import SSH
from io import StringIO
import subprocess
import sys

try:
    ssh = SSH("myhost.example.org")
except subprocess.CalledProcessError as e:
    print(e.stderr.decode('utf-8'), file=sys.stderr)
    raise e

# Run command using the hosts stdin/stdout/stderr
ssh.run("echo 'Hello, World!'")

# Save command output
output = StringIO()
ssh.run("echo 'Hello, World!'", stdout=output)
print(output.getvalue()) # prints Hello, World!

ssh.close()
```

## License

[Apache License 2.0](https://choosealicense.com/licenses/apache-2.0/)