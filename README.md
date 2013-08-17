About
-----
Swagger.py is a Python library for using [Swagger][] defined API's.

Swagger itself is best described on the Swagger home page:

> Swagger is a specification and complete framework implementation for
> describing, producing, consuming, and visualizing RESTful web
> services.

The [Swagger specification][] defines how API's may be described using
Swagger.

Usage
-----
Install swagger.py using the `setup.py` script.

    $ sudo ./setup.py install

This installs the swagger.py libraries, and a `swagger-codegen` tool
for generating code from a set of Swagger API docs.

swagger-codegen
===============

Inspired by the original [swagger-codegen][] project, templates are
written using [Mustache][] templates ([Pystache][], specifically).
There are several important differences.

 * The model that is fed into the mustache templates is almost
   identical to Swagger's API resource listing and API declaration
   model. The differences are listed [below](#model).
 * The templates themselves are completely self contained, with the
   logic to enrich the model being specified in `translate.py` in the
   same directory as the `*.mustache` files.

<a id="model"></a>
Data model
==========

The data model presented by the `swagger_model` module is nearly
identical to the original Swagger API resource listing and API
declaration. This means that if you add extra custom metadata to your
docs (such as a `_author` or `_copyright` field), they will carry
forward into the object model. I recommend prefixing custom fields
with an underscore, to avoid collisions with future versions of
Swagger.

There are a few meaningful differences.

 * Resource listing
   * The `file` and `base_dir` fields have been added, referencing the
     original `.json` file.
   * The objects in a `resource_listing`'s `api` array contains a
     field `api_declaration`, which is the processed result from the
     referenced API doc.
 * API declaration
   * A `file` field has been added, referencing the original `.json`
     file.
   * The `model` field was changed from an object to an array, so it
     can be better referenced from a mustache template.
   * Similarly, a `model`'s `properties` field was changed from an
     object to an array.

Development
-----------

The code is documented using [Epydoc][], which allows [IntelliJ IDEA][]
to do a better job at inferring types for autocompletion.

To keep things isolated, I also recommend installing (and using)
[virtualenv][]. Some scripts are provided to help keep the
environments manageable

    $ sudo pip install virtualenv
    $ ./make-env.sh
    $ . activate-env.sh

[Setuptools][] is used for building.

    $ ./setup.py develop   # prep for development (install deps, launchers, etc.)
    $ ./setup.py nosetests # run unit tests
    $ ./setup.py bdist_egg # build distributable

[Nose][] is used for unit testing, with the [coverage][] plugin
installed to generated code coverage reports. Pass `--with-coverage`
to generate the code coverage report. HTML versions of the reports are
put in `cover/index.html`.


License
-------

Copyright (c) 2013, Digium, Inc.
All rights reserved.

Swagger.py is licensed with a [BSD 3-Clause License][BSD].

 [bsd]: http://opensource.org/licenses/BSD-3-Clause
 [coverage]: http://nedbatchelder.com/code/coverage/
 [epydoc]: http://epydoc.sourceforge.net/
 [intellij idea]: http://confluence.jetbrains.net/display/PYH/
 [mustache]: http://mustache.github.io/
 [nose]: http://nose.readthedocs.org/en/latest/
 [pystache]: https://github.com/defunkt/pystache
 [setuptools]: http://pypi.python.org/pypi/setuptools
 [Swagger specification]: https://github.com/wordnik/swagger-core/wiki
 [swagger-codegen]: https://github.com/wordnik/swagger-codegen
 [swagger]: https://developers.helloreverb.com/swagger/
 [virtualenv]: http://www.virtualenv.org/