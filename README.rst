Python Template Repo
====================

Python Template Repo aims to help you **quickly jumpstart new Python libraries with
integrated developer tooling**. Try this template out if you intend on **distributing
your Python library as an open-source Anaconda package** and **don't want to deal with
the repository infrastructure**!

Simply follow the "Getting Started" guides below. It is also easily configurable based
on your library's needs.

Features
--------

.. raw:: html

   <p align="center">
      <img src="./docs/_static/python-logo.png" alt="Python logo" style="width:200px;"/>
      <img src="./docs/_static/anaconda-logo.webp" alt="Anaconda logo" style="width:200px;"/>
    </p>

- **Python library boilerplate** code using standard practices
- **Unit testing framework** using ``pytest``
- **Quality assurance tooling** (code formatting and linting)
- **Sphinx documentation** with Read the Docs Sphinx Theme
- **GitHub Actions** to run CI/CD workflows for unit testing and quality assurance
- **GitHub Issue and Pull Request templates** for organized ticket tracking
- **Anaconda environments** defined in ``.yml`` files for determinism
- Licensed with **Apache-2.0** and ``.gitignore`` tailored to Python projects

Getting Started
---------------

1. Set up the Python Library
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Follow the steps below to get this repository tailored to your library.

1. On this page, click "Use this template" and "Create a new repository"

   .. image:: docs/_static/use-this-template.png

2. Clone your new repository

   .. code-block:: console

      git clone https://github.com/<USERNAME>/<REPO-NAME>

3. Update ``setup.py`` to replace ``python_template`` references with your project name
4. Rename ``/python_template``, ``python_template.py``, and ``test_python_template.py`` to
   your project name

2. Set up the Anaconda Development Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Follow the steps below to get the Anaconda development environment set up for your
library. We recommend using `mamba`_ instead of ``conda`` because it is significantly
faster and more reliable.

1. Download and Install Anaconda (Mac OS & Linux)

   .. code-block:: console

       curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-$(uname)-$(uname -m).sh"
       bash Mambaforge-$(uname)-$(uname -m).sh

2. Update ``/conda-env/*.yml`` by follow each file's ``#TODO`` comments (don't worry, it's straightforward)

3. Create and activate the Conda development environment

   .. code-block:: console

      mamba env create -f conda-env/dev.yml
      mamba activate template-dev

.. _mamba: https://mamba.readthedocs.io/en/latest/

3. Set up the Documentation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The library's documentation is setup with `Sphinx`_ and `Read the Docs Sphinx Theme`_.

You just need to do a few things to get up and running:

1. Update ``README.rst``, ``AUTHORS.rst``, ``HISTORY.rst``, and ``/docs/index.rst`` as needed
2. Decide how to deploy the documentation. Follow the instructions in the provided links.

   - Option 1: `Read the Docs`_
   - Option 2: `GitHub Pages`_ (via GitHub Actions)

.. _Read the Docs: https://docs.readthedocs.io/en/stable/tutorial/index.html
.. _GitHub Pages: https://coderefinery.github.io/documentation/gh_workflow/

To build the documentation locally (useful for reviewing):

1. Activate the conda developer environment

   .. code-block:: console

      mamba activate template-dev

2. Build documentation

   - Option 1: ``make docs`` from the root of repo (also cleans up and opens docs in your browser)
   - Option 2: ``cd docs && make html``

.. _Sphinx: https://www.sphinx-doc.org/en/master/
.. _Read The Docs Sphinx Theme: https://sphinx-rtd-theme.readthedocs.io/en/stable/

4. Set up Quality Assurance Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This repository includes quality assurance (QA) tools for code formatting (``black``,
``isort``), linting (``flake8``), and unit testing (``pytest``). These tools ensure
that you can easily catch issues and follow good Python practices without sacrificing
energy on them. These tools are integrated in the `pre-commit`_ package as "hooks" that
automatically run when committing changes to files.

To run these QA tools through ``pre-commit``:

1. Activate the conda development environment

   .. code-block:: console

      mamba activate template-dev

2. Install ``pre-commit`` hooks into the Git repository

   .. code-block:: console

      $ pre-commit install
      pre-commit installed at .git/hooks/pre-commit

   - ``pre-commit`` will now run automatically on ``git commit``!

3. (optional) Run against all files

   - it's usually a good idea to run the hooks against all of the files when adding new hooks (usually pre-commit will only run on the changed files during git hooks)

   .. code-block:: console

      $ pre-commit run --all-files
      [INFO] Initializing environment for https://github.com/pre-commit/pre-commit-hooks.
      [INFO] Initializing environment for https://github.com/psf/black.
      [INFO] Installing environment for https://github.com/pre-commit/pre-commit-hooks.
      [INFO] Once installed this environment will be reused.
      [INFO] This may take a few minutes...
      [INFO] Installing environment for https://github.com/psf/black.
      [INFO] Once installed this environment will be reused.
      [INFO] This may take a few minutes...
      Check Yaml...............................................................Passed
      Fix End of Files.........................................................Passed
      Trim Trailing Whitespace.................................................Failed
      - hook id: trailing-whitespace
      - exit code: 1

      Files were modified by this hook. Additional output:

      Fixing sample.py

      black....................................................................Passed

Useful commands:

- Override ``pre-commit`` checks: ``git commit -m <MESSAGE> --no-verify``
- Run individual hook: ``pre-commit run --all-files <black|flake8|isort>``

Information on QA tools:

- `pre-commit`_ - "Git hook scripts are useful for identifying simple issues before
  submission to code review."
- `black`_ - "The uncompromising code formatter" that "will save time and mental energy
  for more important matters".
- `isort`_ - isort is a Python utility / library to sort imports alphabetically, and
  automatically separated into sections and by type.
- `flake8`_ - A Python linter for enforcing a style guide with PEP (Python Enhancement
  Proposals).

.. _pre-commit: https://pre-commit.com/
.. _black: https://black.readthedocs.io/en/stable/
.. _isort: https://pycqa.github.io/isort/
.. _flake8: https://flake8.pycqa.org/en/latest/

Helpful Knowledge
-----------------

How GitHub Actions is Used for CI/CD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This repository uses GitHub Actions to run the CI/CD build workflow. This workflow is
**automatically triggered** with **commits on pull requests to** ``main`` and **merging pull requests to** ``main``.

Jobs include:

1. Run ``pre-commit`` for formatting, linting, and type checking
2. Build conda CI/CD environment with different Python versions, build and install
   the package, and run unit test suite with ``pytest``

*To save time and resources on build cycles, GitHub Actions has been configured to
automatically skip jobs instead of re-executing based on the files that are committed. For
example, if docs are committed, then the unit tests will not run.*

Additional Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Feel free to modify the configuration for QA tools in ``pyproject.toml`` and ``setup.cfg``
- You can also remove some or all the QA tools if you want (not recommended though).
  Just make sure to delete them from your Anaconda ``.yml`` files and remove their entries
  in ``pre-commit-config.yaml`` and their configs in ``pyproject.toml`` and/or ``setup.cfg``
