las_extractor
=============
A Python webframework to extract LAS data to json
=============

License
---------------

GNU General Public License, see LICENSE


Requirements
---------------

* Python 2.6-2.7
* Fusion Tools (see http://forsys.cfr.washington.edu/fusion/fusionlatest.html, freeware, unknown license...)
* LAStools (see http://www.cs.unc.edu/~isenburg/lastools/, LGPL license with restrictions, please check out the license)

Fusion and LAStools are Windows programs. They might run (not tested) under Linux using Wine.

For Linux, simply add `liblas` into `setup.py`:

```
setup(
    ...
    install_requires=[
        ...
+        'liblas'
    ],
```

* PostgreSQL/PostGIS database containing a schema `lidar_tile_index` which should contain a table `grid50mfull`. This table contains polygons describing the tiling of your LAS files. See the <a href="https://github.com/sitn/las_extractor/wiki/Create-the-DB-table" target=_blank>wiki</a> for a better description on how to create this table.

Getting Started
---------------

To install the application:

* Clone this repository:

```
git clone https://github.com/sitn/las_extractor.git
```

* Run Bootstrap:

```
cd las_extractor
python bootstrap-buildout.py --buildout-version 2.3.0 --allow-site-packages
```

* Before running buildout, you will need to create your own buildout file:

```
cp buildout.cfg buildout_<project>.cfg
```

* Delete everthing except the `[vars]` section in your buildout file
* Once done add the following code on top of your buildout file:

```
[buildout]
extends = buildout.cfg
```

* In the `[vars]` section, replace all `overwriteme` values with your own values (see <a href="https://github.com/sitn/las_extractor/wiki/Buildout-vars" target=_blank>wiki</a> for values signification)

* Run buildout:

```
./buildout/bin/buildout -c buildout_<project>.cfg
```

* Add the Apache folder in your Apache conf file (needs the mod_wsgi to be active):
```
Include <project_folder>/apache/*.conf
```

This application uses the Pyramid webframework. For more details, please refer to the <a href="http://docs.pylonsproject.org/projects/pyramid" target=_blank>pyramid documentation</a>.
