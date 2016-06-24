Installing Geospatial Python Packages for OSGeo4W 
=================================================

This is guide for OSGeo4W users on installing some of the harder to
install Python GIS and Geospatial packages.  Hopefully, get packages
working.
[OSGeo4W](https://trac.osgeo.org/osgeo4w/) is an easy way to install
open source GIS software including GDAL and QGIS on Windows.

Any prompts shown below are intended for the OSGeo4W shell.


First Steps
===========

pip and setuptools
------------------

pip and setuptools are software that install packages fairly easily.
pip downloads the package metadata stored on the
[PyPI website](https://pypi.python.org/pypi).

Check to see if pip is installed:
```
C:\...>pip --version
pip 7.1.2 from C:\OSGeo4W\apps\Python27\lib\site-packages (python 2.7)
```

Check your python version:
```
C:\...>python --version
Python 2.7.4
```

In Python 2.7.9 or greater, pip and setuptools my be included in the
default installation.  Since this version is lower, pip and setuptools
 has to be installed.  See [installing pip and setuptools]
(https://pip.pypa.io/en/latest/installing/#install-pip).

Just see if `pip` works on the command line.  Having a recent
version may make a difference.



Microsoft Visual C++ Compiler for Python 2.7
--------------------------------------------
You may will only need this if you need to compile C/C++ code to install
a package.

If you get the error message "Unable to find vcvarsall.bat" when trying
to install a pacakge, this should remedy it.

By installing [Microsoft Visual C++ Compiler for Python 2.7]
(http://www.microsoft.com/en-us/download/details.aspx?id=44266) it will 
allow your machine to compile these packages.

Development Versions
--------------------
If you want to install development versions of the library, please refer to 
the packages installation instruction or its development page.

Binaries
--------
There are binaries available that make it much easier to install.  These
binaries are called wheels.
[Here are some unofficial binaries](http://www.lfd.uci.edu/~gohlke/pythonlibs/).
There is no guarantee the binaries those binaries will work.  Your results
may vary.

numpy, and SciPy
----------------

You may want to install numpy, and SciPy separately from other
packages.  numpy is a requirement for some python geospatial packages
It is easiest to install numpy and SciPy through setup.
```
C:\...> setup
```

matplotlib
----------

matplotlib requires numpy

You may want to install matplotlib separately from other
packages.  Install matplotlib through setup.
```
C:\...> setup
```


Installing Packages
===================
How to Install Python Only Packages
-----------------------------------
Many python packages that do not interface with a C/C++ library.  Simply
install with pip.
```
C:\...> pip install packagename
```

For example pyshp, reads the shapefile format but is entirely coded in
python.  So, to install it simply:
```
C:\...> pip install pyshp
```

Some python packages are very easy to install.

basemap
-------
Install [matplotlib](#matplotlib) and [numpy](#numpy-and-scipy).

In versions of basemap 1.0.8 or greater you will have to additionally install
[pyproj](#pyproj) and pyshp.  Pyproj will need PROJ4 with the inverse
hammer transform, which basemap needs.  Which should be in PROJ.4 version
4.9.3 or greater. Otherwise use the provided copy of pyproj.
```
C:\...> pip install pyshp
```

Install GEOS through packages (packagename: geos): 
```
C:\...> setup
```

Download .tar.gz archive file for [basemap](https://pypi.python.org/pypi/basemap/).

Uncompress file to a folder:
```
C:\...> tar zxf basemap-1.0.7.tar.gz
```

This sets up the GEOS library version to the one in OSGeo4W on the machine.  To install:
```
C:\...> cd basemap-1.0.7
C:\...\basemap-1.0.7> set GEOS_DIR=C:\OSGeo4W
C:\...\basemap-1.0.7> pip install .
```


Fiona
-----

Fiona makes reading/writing GIS vector data from files pretty easy.

[Fiona on PyPi](https://pypi.python.org/pypi/Fiona)

Install requirements GDAL (package name: gdal) through setup:
```
C:\...> setup
```

Install Cython:
```
C:\...> pip install Cython
```

Install all the requirements ([requirements.txt]
(https://github.com/Toblerity/Fiona/blob/master/requirements.txt))
```
C:\...> pip install -r requirements.txt
```

Install [Microsoft Visual C++ Compiler for Python 2.7]
("#microsoft-visual-c-compiler-for-python-27), if you have not already 
installed it.


```
set PATH=%PATH%;C:\OSGeo4W\share\gdal
python setup.py build_ext -IC:\OSGeo4W\include -lgdal_i -LC:\OSGeo4W\lib
python setup.py install
```


Geopandas
---------
[Geopandas on PyPi](https://pypi.python.org/pypi/Geopandas)

Install [matplotlib](#matplotlib) and [numpy](#numpy-and-scipy).

Install [Fiona](#fiona).

Install pandas separately, which has 
[quite a few dependencies many are optional](https://github.com/pydata/pandas#dependencies).
Maybe just:
```
C:\...> pip install pandas
```

Install all the requirements  ([requirements.txt]
(https://github.com/geopandas/geopandas/blob/master/requirements.txt))
```
C:\...> pip install -r requirements.txt
```

Install geopandas
```
C:\...> pip install geopandas
```

Tests are not installed
```
C:\...> py.test tests
```

pyproj
------
pyproj is a library to transform points from one projection (CRS) into
another projection (CRS).  Also, it performs great circle distance
calculations.

[pyproj on PyPi](https://pypi.python.org/pypi/pyproj)

pyproj requires [PROJ 4.9.0](https://github.com/OSGeo/proj.4) or greater.
(Required for the great circle distance calculations [Geod class].)

There are two different ways to install pyproj.  One uses the OSGeo4W
version of library PROJ.4 the other compiles a copy of PROJ.4 (the 
default installation).  The copy included with pyproj includes a
patch for the hammer projection for an inverse (which is useful for
basemap and world projection).  Many users will be fine without it.

**Instruction for using the OSGeo4W PROJ.4 (no compiling):**
* Download pyproj
* unzip
* Install:
```
C:\...> set PROJ_DIR=C:\OSGeo4W\
C:\...\pyproj> pip install .
```

**Instruction for compiling pyproj with included version of PROJ.4:**
* install [Microsoft Visual C++ Compiler for Python 2.7]
("#microsoft-visual-c-compiler-for-python-27), if you have not already 
installed it.
then run:
```
C:\...> pip install pyproj
```

Shapely
-------
[Shapely on PyPi](https://pypi.python.org/pypi/Shapely)

**Via Pip**
(Install version 1.5.16+)
* In the folder `C:\OSGeo4w\bin\`, make a copy `geos_c.dll` and name it `geos.dll`.
```
C:\...> set GEOS_CONFIG=C:\OSGeo4W\bin\
C:\...> pip install shapely
```

**Via Setup**
(Install version 1.2.18)
Install shapely (package name: python-shapely) through setup:
```
C:\...> setup
```

Uninstall/Upgrade packages
----------------------------------
To uninstall simply,
```
C:\...> pip uninstall packagename
```

To upgrade a package,
```
C:\...> pip install -U packagename
````

It should be fairly easy.


Packages Not Covered
====================
- descartes
- rasterio
- rtree
   - requires libspatialindex which can be installed through `setup`

Please submit your pull request to improve this document.

Questions/Improvements
======================
These are a reflection of the packages that I use the most, so there are
many others that I have very little interest in.

Post an issue for questions or improvements.

If you have improvements do a Pull Request.
