======================================
Selecting a Python Version For a Shell
======================================


On a Unix-like OS it's easy to setup you shell to activate a specific version
of Python, and have commands to select another version, allowing you to switch
from one version of Python to another.

I describe the technique I am using on a macOS Mojave system that uses Bash
shell.

The Python control scripts in ~/bin
===================================

I have the ``~/bin`` directory on my PATH, where I sore a set of control
scripts.  For Python I have a set of scripts named ``envfor-pythonX`` where
``X`` is the version of Python to activate.  These scripts do no install
Python, they use and activate a version of Python already installed.

On my system i have the following scripts:

- ``~/bin/envfor-python2``
- ``~/bin/envfor-python3``

The first one activates Python 2.7.16, and the second activates Python
3.8.5. Eventually if I decide to try Python 3.9 I might create a script named
``envfor-python3.9`` and when I'm OK to make 3.9 my main Python version I would
update ``envfor-python3`` to activate Python 3.9.

The following section show the content of each of my scripts:


envfor-python2 script
---------------------

.. code:: shell

    #!/bin/sh
    #  SH FILE: envfor-python2
    #
    #  Purpose   : Activate Python 2.7.
    #  Created   : Sunday, October  4 2020.
    #  Author    : Pierre Rouleau <prouleau001@gmail.com>
    #  Time-stamp: <2020-10-05 14:55:24, updated by Pierre Rouleau>
    # ----------------------------------------------------------------------------
    #  Module Description
    #  ------------------
    #
    # The default Bash shell does not necessarily  provide access to the Python
    # version I need.  Apple controls the version of macOS system's Python.
    # Currently this is Python 2.7.16 located in /usr/bin/python

    # ----------------------------------------------------------------------------
    #  Code
    #  ----
    echo "Using Python 2.7.16 (Apple's System Python)  - Run which-python for more info."

    PATH=${ORIGINAL_PATH}:~/dev/python/apps
    export PATH

    PYTHONPATH=~/dev/python:~/tools/python:/usr/local/lib/python2.7/site-packages:/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python
    export PYTHONPATH

    # -----------------------------------------------------------------------------


envfor-python3 script
---------------------

    #!/bin/sh
    #  SH FILE: envfor-python3
    #
    #  Purpose   : Activate Python 3.
    #  Created   : Monday, October  5 2020.
    #  Author    : Pierre Rouleau <prouleau001@gmail.com>
    #  Time-stamp: <2020-10-05 14:05:18, updated by Pierre Rouleau>
    # ----------------------------------------------------------------------------
    #  Module Description
    #  ------------------
    #
    # Setup to use Python 3.8.5 in the shell as ``python`` with support for pip.

    # Reference
    # - Python 3 installation guide: https://docs.python-guide.org/starting/install3/osx/#install3-osx
    # - Homebrew page on Python:  https://docs.brew.sh/Homebrew-and-Python

    # ----------------------------------------------------------------------------
    #  Code
    #  ----
    echo "Using Python 3.8.5 - Run which-python for more info."

    PATH=/usr/local/opt/python/libexec/bin:${ORIGINAL_PATH}:~/dev/python/apps
    export PATH

    PYTHONPATH=~/dev/python:~/tools/python
    export PYTHONPATH

    # ----------------------------------------------------------------------------


ORIGINAL_PATH and Alias commands
--------------------------------

Executing a Bash script normally will not change the values of environment
variables in the calling script.  To do that the scripts must be sourced.

In my ``~/.bashrc`` I create a set of alias commands for that purpose:


.. code:: shell

    # Python shortcuts
    # ----------------
    alias use-python2='source envfor-python2'
    alias use-python3='source envfor-python3'

The two *envfor-python* scripts set the PATH using the environment variable
``ORIGINAL_PATH``.  This is set to the value of PATH.  This allows using the
use-python2 and use-python3 several times.

Inside the ``~./bash_profile`` the PATH is set and then the following line
remembers its value in the ``ORIGINAL_PATH`` environment variable.

.. code:: shell

    export ORIGINAL_PATH=${PATH}



Selecting A default Python for a Shell
--------------------------------------

I select Python 3 as my default for by Bash shells.

All I need to do is source ``~/bin/envfor-python3`` inside my
``~.bash_profile``.

My ``~.bash_profile`` starts by sourcing the content of my ``~/.bashrc`` file:


.. code:: shell

    # Shell command shortcuts
    # =======================
    #
    # Some quick command shortcuts.  Identified by .bashrc:

    source $HOME/.bashrc


Later in ``~/.bash_profile`` I have the code that selects the version of
Python that will be available right from the start of the shell:

.. code:: shell

    # Python settings
    # ===============

    source ~/bin/envfor-python3


Python inside Bash Shell
------------------------

Here's a snapshot of a session.  When the shell starts, Python 3.8.5 is
available.  Then I switch to using Python 2.7.16 and then switch again to
Python 3.8.5.

.. code:: shell

    Last login: Mon Oct  5 15:18:37 on ttys018
    Using Python 3.8.5 - Run which-python for more info.
    >Pierres-Cpu@Mon Oct 05@15:20:48[~]
    > python
    Python 3.8.5 (default, Jul 21 2020, 10:42:08)
    [Clang 11.0.0 (clang-1100.0.33.17)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> exit()
    >Pierres-Cpu@Mon Oct 05@15:20:58[~]
    > use-python2
    Using Python 2.7.16 (Apple's System Python)  - Run which-python for more info.
    >Pierres-Cpu@Mon Oct 05@15:21:03[~]
    > python
    Python 2.7.16 (default, Jan 27 2020, 04:46:15)
    [GCC 4.2.1 Compatible Apple LLVM 10.0.1 (clang-1001.0.37.14)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> exit()
    >Pierres-Cpu@Mon Oct 05@15:21:15[~]
    > use-python3
    Using Python 3.8.5 - Run which-python for more info.
    >Pierres-Cpu@Mon Oct 05@15:21:23[~]
    > python
    Python 3.8.5 (default, Jul 21 2020, 10:42:08)
    [Clang 11.0.0 (clang-1100.0.33.17)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> exit()
    >Pierres-Cpu@Mon Oct 05@15:21:28[~]
    >
