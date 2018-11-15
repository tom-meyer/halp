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
