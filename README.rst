Electron Cash - Lightweight Bitcoin Cash client
=====================================

::

  Licence: MIT Licence
  Author: Jonald Fyookball
  Language: Python
  Homepage: https://electroncash.org/


.. image:: https://d322cqt584bo4o.cloudfront.net/electron-cash/localized.svg
    :target: https://crowdin.com/project/electron-cash
    :alt: Help translate Electron Cash online





Getting started
===============

Electron Cash is a pure python application forked from Electrum. If you want to use the
Qt interface, install the Qt dependencies::

    sudo apt-get install python3-pyqt5

If you downloaded the official package (tar.gz), you can run
Electron Cash from its root directory (called Electrum), without installing it on your
system; all the python dependencies are included in the 'packages'
directory. To run Electron Cash from its root directory, just do::

    ./electron-cash

You can also install Electron Cash on your system, by running this command::

    sudo apt-get install python3-setuptools
    python3 setup.py install

This will download and install the Python dependencies used by
Electron Cash, instead of using the 'packages' directory.

If you cloned the git repository, you need to compile extra files
before you can run Electron Cash. Read the next section, "Development
Version".



Development version
===================

Check out the code from Github::

    git clone https://github.com/Electron-Cash/Electron-Cash
    cd Electron-Cash

Run install (this should install dependencies)::

    python3 setup.py install

Compile the protobuf description file::

    sudo apt-get install protobuf-compiler
    protoc --proto_path=lib/ --python_out=lib/ lib/paymentrequest.proto

Create translations (optional)::

    sudo apt-get install python-requests gettext
    ./contrib/make_locale

Compile libsecp256k1 (optional, yet highly recommended)::

    ./contrib/make_secp

For plugin development, see the `plugin documentation <plugins/README.rst>`_.

Running unit tests::

    pip install tox
    tox

Tox will take care of building a faux installation environment, and ensure that
the mapped import paths work correctly.

Creating Binaries
=================


To create binaries, create the 'packages/' directory::

    ./contrib/make_packages

This directory contains the python dependencies used by Electron Cash.

The `make_packages` command may fail with some Ubuntu-packaged versions of
pip ("can't combine user with prefix."). To solve this, it is necessary to
upgrade your pip to the official version::

    pip install pip --user

**Note:** You should also compile the secp256k1 library for fast elliptic curve
cryptographic functions. Otherwise, transaction signing will be extremely slow,
and you won't have access to the CashShuffle functionality of Electron Cash::

    ./contrib/make_secp

This will install ``libsecp256k1.so.0`` into the ``lib/`` folder.

Linux (source with packages)
----------------------------

Run the following to create the release tarball under ``dist/``::

    ./setup.py sdist --enable-secp

This command will *NOT* run the above ``make_locale`` and ``make_packages`` for
you, so you should run them if you want to include Python packages and
translations in the srcdist.  It will, however run ``make_secp`` for you and
it will bundle libsecp256k1-0 into the aforementioned release tarball.

Mac OS X / macOS
--------

See `contrib/osx/ <contrib/osx/>`_.

Windows
-------

See `contrib/build-wine/ <contrib/build-wine>`_.

Android
-------

See the file `gui/kivy/Readme.txt <gui/kivy/Readme.txt>`_.

iOS
-------

See `ios/ <ios/>`_.
