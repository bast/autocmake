# Autocmake

A CMake plugin composer.

## Bootstrapping a new project

Bootstrap a CFrame infrastructure out of "nothing":

    mkdir cmake  # does not have to be called "cmake" - take the name you prefer
    cd cmake
    wget https://github.com/scisoft/autocmake/raw/master/bootstrap.py
    python bootstrap.py --init

This downloads and creates the following files:

    cmake/
    ├── bootstrap.py   # no need to edit
    ├── cframe.cfg     # edit this file
    └── lib/
        ├── config.py  # no need to edit
        └── docopt.py  # no need to edit

If you use version control, then now is a good moment to status/diff/add
the newly created files.

## Creating the CMake infrastructure

Then edit ``cframe.cfg`` and run the ``bootstrap.py`` script which
creates ``CMakeLists.txt`` and ``setup.py`` in the path specified (here ".."):

    python bootstrap.py ..

The script also copies or downloads CMake modules specified in ``cframe.cfg`` to a directory
called ``modules/``:

    cmake/
    ├── bootstrap.py
    ├── cframe.cfg
    └── lib/
        ├── config.py
        └── docopt.py
        └── modules/   # CMakeLists.txt includes CMake modules from this directory

Now you have ``CMakeLists.txt`` and ``setup.py`` in the project root and you can build
the project:

    cd ..
    python setup.py [-h]
    cd build
    make

## Customizing the CMake modules

The CMake modules can be customized directly inside ``modules/`` but this is
not very convenient as the customizations may be overwritten by the
``boostrap.py`` script.

A better solution is to download the CMake modules that you wish you customize
to a separate directory and source the customized CMake modules in
``cframe.cfg``.