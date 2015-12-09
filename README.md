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
Install matplotlib and numpy (see above).

In versions of basemap 1.0.8 or greater you will have to install pyproj
(see section below) and pyshp: 
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

Install requirements GDAL (package name: gdal) and shapely (package name:
python-shapely) through setup:
```
C:\...> setup
```

Install all the requirements ([requirements.txt]
(https://github.com/Toblerity/Fiona/blob/master/requirements.txt))
```
C:\...> pip install -r requirements.txt
```


Geopandas
---------
[Geopandas on PyPi](https://pypi.python.org/pypi/Geopandas)

Install `numpy` and `SciPy` through setup.
```
C:\...> setup
```

Install Fiona (see above).

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

pyproj
------
pyproj is a library to transform points from one projection (crs) into
another projection (crs).  Also, it performs great circle distance
calculations.

[pyproj on PyPi](https://pypi.python.org/pypi/Geopandas)

pyproj requires PROJ 4.9.0 or greater.  (Required for the Geod class.)

There are two different ways to install pyproj.  One uses the OSGeo4W
version of library PROJ.4 the other compiles a copy of PROJ.4 (the 
default installation).  The copy included with pyproj includes a
patch for the hammer projection for an inverse (which is useful for
basemap and world projection).  Many users will be fine without it.

Instruction for using the OSGeo4W PROJ.4 (no compiling):
* Download pyproj
* unzip
* Install:
```
C:\...> set PROJ_DIR=C:\OSGeo4W\
C:\...\pyproj> python setup-proj.py install
```

Instruction for compiling pyproj with included version of PROJ.4: 
# install Microsoft Visual C++ Compiler for Python 2.7 (see above), 
if you have not already installed it.
```
C:\...> pip install pyproj
```

Shapely
-------
[Shapely on PyPi](https://pypi.python.org/pypi/Shapely)

Install  shapely (package name: python-shapely) through setup:
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

Please submit your pull request to.

Questions/Improvements
======================
These are a reflection of the packages that I use the most, so there are
many others that I have very little interest in.

Post an issue for questions or improvements.

If you have improvements do a Pull Request.
