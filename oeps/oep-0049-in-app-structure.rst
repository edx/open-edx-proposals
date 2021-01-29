
=============================
OEP-0049: Django App Patterns
=============================

.. list-table::
   :widths: 25 75

   * - OEP
     - :doc:`OEP-0045 </oeps/oep-0049>`
   * - Title
     - Django App Patterns
   * - Last Modified
     - 2021-01-29
   * - Authors
     - Matt Tuchfarber <mtuchfarber@edx.org>
   * - Arbiter
     - TBD
   * - Status
     - Draft
   * - Type
     - Architecture
   * - Created
     - 2021-01-29
   * - Review Period
     - TBD

Abstract
--------
As our number of Django apps continue to grow in our many services, we want to coalesce around a couple of standard design patterns to both make switching between codebases easier and to help untangle some of the links between codebases we have today. These decisions should be considered "best practices" or the default patterns, and should only be violated if the code base requires it.

Decision
--------

All of our Django apps should have a common structure. This consists of a combination of default Django-style code and Open edX-specific code. Listed below are each of the files or folders your app should contain and what they should consist of.

README.rst
++++++++++
Each app should contain a README.rst to explain it's use. See full details of what should go in the README.rst in OEP-0019_

.. _OEP-0019: https://open-edx-proposals.readthedocs.io/en/latest/oep-0019-bp-developer-documentation.html#readmes

__init__.py
+++++++++++
The ``__init__.py`` file should either be blank if the app is a plugin, or contain a single line defining the ``default_app_config`` for the app. This ``default_app_config`` should point to the ``AppConfig`` located in ``<app_name>/apps.py``.

Unlike many packages, ``__init__.py`` should *not* be used to as the way to export the app's public methods. These should be exported using ``api.py`` (and thus imported as ``from path.to.app.api import public_function``). See ``api.py`` below.

For example:

.. code-block:: python

    default_app_config = "service_name.apps.app_name.apps.CustomAppConfig"



apps.py
+++++++
The ``apps.py`` file should contain a subclass of a Django ``AppConfig``. The AppConfig should set the app's name to it's full path (e.g. ``name = "service_name.apps.app_name"``) and should (optionally) have an overriding ``ready()`` function which initializes the app. This initialization also often includes setting up Django signals.

For example:

.. code-block:: python

    class MyAppConfig(AppConfig):
        """
        Application Configuration for MyApp.
        """
        name = "service_name.apps.app_name"

        # (optional) Set up plugin. See https://github.com/edx/edx-django-utils/tree/master/edx_django_utils/plugins

        def ready(self):
            """
            Connect handlers to recalculate grades.
            """
            from .signals import handlers

api.py
++++++
This should be single point of entry for other Python code to talk to your app. This is *not* a Rest API, this is a Python API. Some rules for ``api.py`` are as follows:

1. API methods defined in ``api.py`` should be well-named, self-consistent, and relevant to its own domain (without exposing technical and implementation details)
2. An app's Django models and other internal data structures should not be exposed via its Python APIs.
3. Ideally, tests should use only Python APIs declared in other apps' ``api.py`` files. However, if an app's API is needed *only* for testing, then test-relevant Python APIs should be defined/exported in an intentional Python module called ``api_for_tests.py``.

Consequences
------------

References
----------
