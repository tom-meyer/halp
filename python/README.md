### Module path

With `inspect`:

    import os
    import inspect
    inspect.getabsfile(os) # path of module
    
    inspect.getabsfile(inspect.currentframe()) # path for current code

There is also the `__file__` attribute, but `inspect` is more reliable.

### Adding to module search path

Given a python module at `/opt/mypy/mymod.py`

    # use environment var
    export PYTHONPATH=/opt/mypy
    python -m mymod

    # place a .pth file in the site-packages dir
    echo /opt/mypy > /usr/lib/python2.7/site-packages/mypy.pth
    python -m mymod

Also there is `sitecustomize`, `usercustomize`, and `USER_SITE`. See https://pymotw.com/2/site/

### The site module

    python -m site # prints useful info about the installation

### Type checking

Type checking is available from 3.5 and on.

Install [mypy][1]:

    pip install mypy

Run on the command line:

    mypy main.py

To use with syntastic, just enable it:

    let g:syntastic_python_checkers=['mypy']

### system exec

    import os
    import shutil
    
    ssh_bin = shutil.which('ssh')
    os.execl(
        ssh_bin, # executable
        ssh_bin, # argv[0]
        '-i', key_file,
        '-o', 'StrictHostKeyChecking=no',
        '-o', 'UserKnownHostsFile=/dev/null',
        '-o', 'HashKnownHosts=no',
        *dst_args,
        *ssh_args,
    )
    
[1]: https://github.com/python/mypy
