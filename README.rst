SeleniumLibrary
===============

.. contents::

Introduction
------------

SeleniumLibrary_ is a web testing library for `Robot Framework`_ that
utilizes the Selenium_ tool internally. The project is hosted on GitHub_
and downloads can be found from PyPI_.

SeleniumLibrary currently works with Selenium 4. It supports Python 3.8 through 3.13.
In addition to the normal Python_ interpreter, it works also
with PyPy_.

SeleniumLibrary is based on the "old SeleniumLibrary" that was forked to
Selenium2Library and then later renamed back to SeleniumLibrary.
See the `VERSIONS.rst`_ for more information about different versions and the
overall project history.

.. image:: https://img.shields.io/pypi/v/robotframework-seleniumlibrary.svg?label=version
   :target: https://pypi.python.org/pypi/robotframework-seleniumlibrary
   
.. image:: https://img.shields.io/pypi/dm/robotframework-seleniumlibrary.svg
   :target: https://pypi.python.org/pypi/robotframework-seleniumlibrary

.. image:: https://img.shields.io/pypi/l/robotframework-seleniumlibrary.svg
   :target: https://www.apache.org/licenses/LICENSE-2.0

.. image:: https://github.com/robotframework/SeleniumLibrary/actions/workflows/CI.yml/badge.svg?branch=master
    :target: https://github.com/robotframework/SeleniumLibrary/actions/workflows/CI.yml

Keyword Documentation
---------------------
See `keyword documentation`_ for available keywords and more information
about the library in general.

Installation
------------

The recommended installation method is using pip_::

    pip install --upgrade robotframework-seleniumlibrary

Running this command installs also the latest Selenium and Robot Framework
versions. The ``--upgrade`` option can be omitted when installing the library for the
first time.

It is possible to install directly from the GitHub_ repository. To install
latest source from the master branch, use this command::

    pip install git+https://github.com/robotframework/SeleniumLibrary.git

Please note that installation will take some time, because ``pip`` will
clone the SeleniumLibrary_ project to a temporary directory and then
perform the installation.

See `Robot Framework installation instructions`_ for detailed information
about installing Python and Robot Framework itself. For more details about
using ``pip`` see `its own documentation <pip_>`__.

Browser drivers
---------------

Browsers and drivers are installed and managed automatically by `Selenium Manager`__.
For more information, see the `Selenium documentation`__.

__ https://www.selenium.dev/documentation/selenium_manager
__ https://seleniumhq.github.io/selenium/docs/api/py/index.html#drivers

Usage
-----

To use SeleniumLibrary in Robot Framework tests, the library needs to
first be imported using the ``Library`` setting as any other library.
The library accepts some import time arguments, which are documented
in the `keyword documentation`_ along with all the keywords provided
by the library.

When using Robot Framework, it is generally recommended to write as
easy-to-understand tests as possible. The keywords provided by
SeleniumLibrary is pretty low level, though, and often require
implementation-specific arguments like element locators to be passed
as arguments. It is thus typically a good idea to write tests using
Robot Framework's higher-level keywords that utilize SeleniumLibrary
keywords internally. This is illustrated by the following example
where SeleniumLibrary keywords like ``Input Text`` are primarily
used by higher-level keywords like ``Input Username``.

.. code:: robotframework

    *** Settings ***
    Documentation     Simple example using SeleniumLibrary.
    Library           SeleniumLibrary

    *** Variables ***
    ${LOGIN URL}      http://localhost:7272
    ${BROWSER}        Chrome

    *** Test Cases ***
    Valid Login
        Open Browser To Login Page
        Input Username    demo
        Input Password    mode
        Submit Credentials
        Welcome Page Should Be Open
        [Teardown]    Close Browser

    *** Keywords ***
    Open Browser To Login Page
        Open Browser    ${LOGIN URL}    ${BROWSER}
        Title Should Be    Login Page

    Input Username
        [Arguments]    ${username}
        Input Text    username_field    ${username}

    Input Password
        [Arguments]    ${password}
        Input Text    password_field    ${password}

    Submit Credentials
        Click Button    login_button

    Welcome Page Should Be Open
        Title Should Be    Welcome Page


The above example is a slightly modified version of an example in a
`demo project`_ that illustrates using Robot Framework and SeleniumLibrary.
See the demo for more examples that you can also execute on your own
machine. For more information about Robot Framework test data syntax in
general see the `Robot Framework User Guide`_.

Extending SeleniumLibrary
-------------------------
Before creating your own library which extends the ``SeleniumLibrary``, please consider would
the extension be also useful also for general usage. If it could be useful also for general
usage, please create a new issue describing the enhancement request and even better if the
issue is backed up by a pull request.

If the enhancement is not generally useful, example solution is domain specific, then the
SeleniumLibrary offers public APIs which can be used to build its own plugins and libraries.
Plugin API allows us to add new keywords, modify existing keywords and modify the internal
functionality of the library. Also new libraries can be built on top of the
SeleniumLibrary. Please see `extending documentation`_ for more details about the
available methods and for examples how the library can be extended.

Community
---------

If the provided documentation is not enough, there are various community channels
available:

- ``#seleniumlibrary`` and ``#seleniumlibrary-dev`` channels in
  Robot Framework `Slack community`_
- `Robot Framework forum`_ has channel for SeleniumLibrary.
- SeleniumLibrary `issue tracker`_ for bug reports and concrete enhancement
  requests
- `Other community channels`_ including paid support


.. _Robot Framework: https://robotframework.org
.. _Selenium: https://www.seleniumhq.org/
.. _SeleniumLibrary: https://github.com/robotframework/SeleniumLibrary
.. _pip: http://pip-installer.org
.. _PyPI: https://pypi.python.org/pypi/robotframework-seleniumlibrary
.. _GitHub: https://github.com/robotframework/SeleniumLibrary
.. _Keyword Documentation: https://robotframework.org/SeleniumLibrary/SeleniumLibrary.html
.. _Python: https://python.org
.. _PyPy: https://pypy.org
.. _demo project: https://github.com/robotframework/WebDemo
.. _Robot Framework User Guide: https://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html
.. _Robot Framework installation instructions: https://github.com/robotframework/robotframework/blob/master/INSTALL.rst
.. _extending documentation: https://github.com/robotframework/SeleniumLibrary/blob/master/docs/extending/extending.rst
.. _Slack community: https://robotframework-slack-invite.herokuapp.com
.. _Robot Framework forum: https://forum.robotframework.org/
.. _issue tracker: https://github.com/robotframework/SeleniumLibrary/issues
.. _Other community channels: https://robotframework.org/#community
.. _VERSIONS.rst: https://github.com/robotframework/SeleniumLibrary/blob/master/VERSIONS.rst

