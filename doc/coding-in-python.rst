================
Coding in Python
================

:Home page: :Home page: https://github.com/pierre-rouleau/about-python
:Time-stamp: <2020-09-04 15:05:36, updated by Pierre Rouleau>
:Copyright:  Copyright © 2020, Pierre Rouleau
:License: `MIT <LICENSE>`_

.. contents::  **Table of Contents**
.. sectnum::

.. ---------------------------------------------------------------------------

Python Code Organization
========================

I write Python code to build different types of programs:

- command line utilities,
- complete GUI applications,
- web servers,
- other types of servers,
- etc...

I prefer to move much of the code logic in re-usable components.
That's Python modules or packages.  In some case organized in libraries.
And I want to be able to re-use these in all the programs I write.

I also want to invoke the command line libraries by their name, on all the
operating systems I use, whether they are Unix-like, Windows or anything else
supported by Python.

I organize my Python code to be able to do that.

Directory Layout
----------------

All the Python code I write that is not a published independent library is
under one directory tree.  Something I can treat as a complete project.

I normally have a directory that contains all my development projects.
I normally call this the **dev** directory.  I've also used ``code`` or
``projects`` but if there's no technical or political reason to ban ``dev`` I
prefer it even though its name is close to the Unix ``/dev`` directory.

- Under Unix-like environment I place this under my home directory, in
  ``~/dev``.
- Under Windows, it depends.  I tend to devote a disk drive to development
  code, the ``D:`` drive if possible, but that depends on the disk drives,
  their speed and the partitions.  Then inside the selected drive I use the
  same directory name, something like ``D:\dev``

Under this:

- For my main Python project that contains the utilities I use all the time, I
  normally call this project **python**.  So that's in ``~/dev/python``.

  - Each program has a main file and one or several launcher files.
    They are all stored inside the **apps** sub-directory

  - Each package has its own directory, at the same level.

  - I normally use the directory ``_doc`` to store documentation.  The name starts
    with an underscore so it shows first in the list of directories.

In my how directory I also have a ``bin`` directory where I store several
generic scripts and executable files, a ``devpub`` directory that contains
clones of public projects repositories.

Overall, it looks like this, assuming I have 3 one-level packages called
``ppr``, ``pprg`` and ``pprm``::

                ~
                ├── bin
                ├── dev
                ├── python
                │   ├── _doc
                │   ├── apps
                │   ├── ppr
                │   ├── pprg
                │   ├── pprm
                │   └── pprx
                └── devpub



.. ---------------------------------------------------------------------------
