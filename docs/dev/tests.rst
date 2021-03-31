=====
Tests
=====


API View Tests
--------------

API View Tests are a collection of all the available API's made up of the individual CRAMS packages.

Running the API view Test Suite
-------------------------------

The API view tests are located in the ``CRAMS_API`` module. 

Make sure to install the python test packages from the ``test-requirements.txt`` into your python environment::

    pip install -r test-requirements.txt

Then run the test using::

    pytest -v 

The argument ``-v`` will increase verbosity of the test is optional.

Module Unit Tests
-----------------

Each module in CRAMS will have its own unit tests that covers the modules models, serializers and view tests.

Running Unit Tests for each module
---------------------------------------------

To the run the unit tests for a module make sure to install the python test packages from the module ``test-requirements.txt`` into your python environment::

    pip install -r test-requirements.txt

Then run the test using::

    pytest -v

The argument ``-v`` will increase verbosity of the test is optional.

Module Test Structure
---------------------

Tests will be stored in a directory of the root module called ``tests``::

    module-package
        + tests
            + test_view.py
            + test_model.py
            + test_serializer.py

You can also specify a specific test to run by parsing the test file::

    pytest -v tests/test_view.py

This will run only the tests in the ``test_view.py`` file.