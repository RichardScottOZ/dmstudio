dmstudio
========

Python module for Datamine scripting. Versions supported are:

* Datamine Studio version 3
* Datamine Studio version RM
* Datamine Studio version EM

The module is made up of the following packages:

* ``dmcommands`` a complete set of of Studio commands that require input files as they appear in the StudioRM.chm help file.
* ``dmfiles`` the remaining Studio commands that do not use input files and are mainly used for generating datamine files
* ``special`` some special functions which are adaptations of Studio commands (coming soon)
* ``superprocess`` special function that involve a string a Studio commands

License
-------

Copyright (c) 2018 Sean D. Horan

See LICENSE.txt for MIT <https://github.com/seanhoran/dmstudio/blob/master/LICENSE.txt> license.

Datamine Commands
-----------------

An exhaustive set of Datamine Studio command is available in the ``dmstudio.dmcommands`` package. The variables consist of four parts:

* Input files
* Output files 
* Fields
* Parameters

The python input variables are identical to the variable names used by Datamine with the following exceptions:

* All variables are lowercase
* Input files have the suffix "_i", output files have the suffix "_o", fields have the suffix "_f" and parameters have the suffix "_p".
* Multiple field selection is entered as a list instead of multiple variables for some commands e.g f1, f2, f3 => fields=[f1, f2, f3]

The ``dmstudio.dmfiles`` package is for commands such as ``INPFIL`` which requires an output file and a string of arguments. The purpose of the ``dmstudio.special`` package is to simplify the usage of some processes such as ``dmstudio.dmfiles.inpfil``. This package is currently a work in progress.

Usage
-----

Using the ``dmstudio.dmcommands`` package:

    >>> from dmstudio import dmcommands
    >>> cmd = dmcommands.studio(version='StudioRM')
    >>> cmd.copy(in_i='fake_model', out_o='fake_model_copy', retrieval='AU>2.0')
    
Using the ``dmstudio.dmfiles`` package:

    >>> from dmstudio import dmfiles
    >>> dmf = dmfiles.studio(version='StudioRM')
    >>> arguments = "'XXXXXXXX'"
    >>> dmf.infile(out_o='points.csv', arguments=arguments)

Initialization
--------------

The COM object is intialized using ``win32client`` package and is passed to a variable ``oScript`` which is consistent with traditional Datamine Studio javascripts or ``vbscript``. Each package is required to be initialized seperatly although in reality they are redundantly initializing the same COM object. There is only a minor impact on processing time which is noticeable only when running scripts on small data sets.
