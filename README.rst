Python Geomark
==============

|PyPi Version|
|License|
|Supported Python Versions|

|Build Status|
|Coveralls Status|
|Requires.io Status|

A small python library that provides implementations of the BC
Governments `Geomark Web
Service <https://www2.gov.bc.ca/gov/content/data/geographic-data-services/location-services/geomark-webservice>`__

Installation
------------

Option 1 - Install with pip
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   Simply install latest version with pip:

   ``pip install geomark``

Option 2 - Clone this repository and install manually
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. We will do our best to keep the master branch of this repository
   stable. However you could also checkout the tag corresponding to
   whichever version x.y.z you would like...

   ``git clone [-b x.y.z] https://github.com/pauperpythonistas/python-geomark.git``

2. the cd into the directory where this repository was cloned

   ``cd /path/to/python-geomark``

3. Install using setup.py

   ``python setup.py install``

4. **Or...** Follow step 1 above then install using pip

   ``pip install /path/to/cloned/python-geomark``

Usage
-----

A Geomark object can be instantiated with either a Geomark ID or a full
Geomark URL.

We recommend using the Geomark ID.

.. code:: python


    from geomark import Geomark

    gm = Geomark('gm-abcdefghijklmnopqrstuv0bcislands')
    # or...
    gm = Geomark('https://apps.gov.bc.ca/pub/geomark/geomarks/gm-abcdefghijklmnopqrstuv0bcislands')

This library supports all of the basic read functions from the Geomark
API.

Reponse results are returned as a bytes string. It can be parsed using
the appropriate library.

The default format is 'json' which will return a json parsable byte
string. When using the JSON format any geometries will be formatted as
EWKT.

Any of the `supported file
formats <https://apps.gov.bc.ca/pub/geomark/docs/fileFormats.html>`__
may be requested.

.. code:: python


    import json
    from geomark import Geomark

    gm = Geomark('gm-abcdefghijklmnopqrstuv0bcislands')

    info = json.loads(gm.info())
    parts = json.loads(gm.parts('geojson'))  # geojson is also supported.

Data can also be requested in any of the `supported coordinate
systems <https://apps.gov.bc.ca/pub/geomark/docs/coordinateSystems.html>`__.

.. code:: python

    import json
    from geomark import Geomark

    gm = Geomark('gm-abcdefghijklmnopqrstuv0bcislands')
    parts_bcalbers = json.loads(gm.parts('geojson', 3005))

If you get data in a format you wish to write to a file you may do so by
simply opening a file location as writable in binary mode. (wb)

.. code:: python

    from geomark import Geomark

    gm = Geomark('gm-abcdefghijklmnopqrstuv0bcislands')
    feature_file = gm.feature('shpz')

    with open('bc_islands.shpz', 'wb') as file:
        file.write(feature_file)

Testing
-------

Using tox
~~~~~~~~~

The recommended way to run the tests is by using
`tox <https://tox.readthedocs.io/en/latest/>`__, which can be installed
using\ ``pip install tox``.

You can use ``tox -l`` to list the available environments, and then e.g.
use the following to run all tests with Python 3.6

::

        tox -e py36

Running tests manually
~~~~~~~~~~~~~~~~~~~~~~

Please refer to the `tox.ini <tox.ini>`__ file for reference/help in
case you want to run tests manually / without tox.

Contributing
------------

1. Fork it!
2. Create your feature branch: ``git checkout -b my-new-feature``
3. Commit your changes: ``git commit -am 'Add some feature'``
4. Push to the branch: ``git push origin my-new-feature``
5. Submit a pull request :D

History
-------

Recent changes can be viewed in the `CHANGES.rst
<https://github.com/pauperpythonistas/python-geomark/blob/master/CHANGES.rst>`__
file.

Credits
-------

-  `Adam Valair <https://github.com/spatialbits>`__ (Primary
   Developer/Maintainer)
-  `Greg Sebastian <https://github.com/gregseb>`__ (Primary
   Developer/Maintainer)

License
-------

This project is licensed under the BSD 3-Clause License - see the
`LICENSE <https://github.com/pauperpythonistas/python-geomark/blob/master/LICENSE>`__ file for details

.. |Build Status| image:: https://travis-ci.org/pauperpythonistas/python-geomark.svg?branch=master
   :target: https://travis-ci.org/pauperpythonistas/python-geomark

.. |Coveralls Status| image:: https://coveralls.io/repos/github/pauperpythonistas/python-geomark/badge.svg?branch=master
   :target: https://coveralls.io/github/pauperpythonistas/python-geomark?branch=master

.. |Requires.io Status| image:: https://requires.io/github/pauperpythonistas/python-geomark/requirements.svg?branch=master
     :target: https://requires.io/github/pauperpythonistas/python-geomark/requirements/?branch=master
     :alt: Requirements Status

.. |PyPi Version| image:: https://img.shields.io/pypi/v/geomark.svg
    :target: https://pypi.python.org/pypi/geomark

.. |Supported Python Versions| image:: https://img.shields.io/pypi/pyversions/geomark.svg
    :target: https://pypi.python.org/pypi/geomark

.. |License| image:: https://img.shields.io/pypi/l/geomark.svg
    :target: https://pypi.python.org/pypi/geomark
