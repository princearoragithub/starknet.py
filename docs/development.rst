Development
===========

This page describes how to setup development environment. You don't need to follow the instructions if you just use starknet.py
as a package.


Development dependencies
------------------------
- `poetry <https://python-poetry.org/>`_ - dependency manager.
- `pyenv <https://github.com/pyenv/pyenv>`_ - recommended for installing and switching python versions locally.

Make sure running ``poetry run python --version`` returns ``Python 3.7.12``.

Setup
-----

.. code-block:: bash

    # Install dependencies
    poetry install

    # Make sure everything was installed properly
    poe test

Crypto-cpp
----------

By default, the library uses ``crypto-cpp`` and so it must be configured properly for development:

1. Compile it from sources (https://github.com/starkware-libs/crypto-cpp)
2. Copy ``libcrypto_c_exports.dylib`` from ``crypto-cpp/src/starkware/crypto/ffi/libcrypto_c_exports.dylib`` to ``starknet_py/utils/crypto``

To use python implementation instead, ``DISABLE_CRYPTO_C_EXTENSION`` environment variable can be set to ``false``

.. code-block:: sh

    export DISABLE_CRYPTO_C_EXTENSION="false"

Git hooks
---------
Run this snippet to enable lint checks and automatic formatting before commit/push.

.. code-block:: bash

    cp pre-push ./.git/hooks/
    cp pre-commit ./.git/hooks/
    chmod +x ./.git/hooks/pre-commit
    chmod +x ./.git/hooks/pre-push

Documentation
-------------
`Sphinx <https://www.sphinx-doc.org/en/master/>`_ is used for generating documentation.

.. code-block:: bash

    # Install additional dependencies for docs
    poetry install -E docs

    # Generate HTML documentation
    poe docs_create

    # Open generated HTML documentation
    poe docs_open

Tests
-----

.. code-block:: bash

    # Run whole suite
    poe test

    # Generate test report in terminal
    poe test_report

    # Generate HTML report and open it in the browser
    poe test_html

    # Run only unit tests
    poe test_unit

    # Run only e2e tests
    poe test_e2e


Running e2e tests in PyCharm
----------------------------
1. Run ``starkware-devnet`` script before running e2e tests in PyCharm.
2. Use ``E2E tests`` configuration to run or debug.

⚠️ **Warning**: Make sure to fill your interpreter in the configuration, to match your project's poetry venv.

