Development environment
=======================

Ready to contribute? Here's how to set up `ansible_rulebook` for local development:

1. Fork the `ansible_rulebook` repo on GitHub.
2. Clone your fork locally

.. code-block:: console

    git clone git@github.com:your_name_here/ansible-rulebook.git

3. We use a rules engine called Drools which is written in Java. From our python code
   we directly call the Drools Java classes using JPY. The following criteria must be
   met for JPY to work correctly:

   * Java 11+ installed
   * Environment variable JAVA_HOME set accordingly
   * Maven 3.8.1+ installed, might come bundled in some Java installs


4. Install your local copy into a virtualenv. Assuming you have virtualenvwrapper installed, this is how you set up your fork for local development:

.. code-block:: console

    cd ansible_rulebook/
    python3.9 -m venv venv
    source venv/bin/activate
    pip install -e .
    pip install -r requirements_dev.txt
    ansible-galaxy collection install ansible.eda

5. Create a branch for local development:

.. code-block:: console

    git checkout -b name-of-your-bugfix-or-feature

Now you can make your changes locally.

6. When you're done making changes, check that your changes pass flake8 and the
   tests, including testing other Python versions with tox:

.. code-block:: console

    flake8 ansible_rulebook tests
    pytest
    tox

To get flake8 and tox, just pip install them into your virtualenv.

7. Commit your changes and push your branch to GitHub:

.. code-block:: console

    git add .
    git commit -m "Your detailed description of your changes."
    git push origin name-of-your-bugfix-or-feature

8. Submit a pull request through the GitHub website.



Building the container image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The dockerfile points to the required collection_ of ansible which provides source plugins.

.. _collection: https://github.com/ansible/event-driven-ansible

.. code-block:: console

    docker build -t localhost/ansible-rulebook:dev .



Git pre-commit hooks (optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To automatically run linters and code formatter you may use
`git pre-commit hooks <https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks>`_.
This project provides a configuration for `pre-commit <https://pre-commit.com/>`_
framework to automatically setup hooks for you.

1. First install the ``pre-commit`` tool:

  a. Into your virtual environment:

     .. code-block:: console

         pip install pre-commit

  b. Into your user directory:

     .. code-block:: console

         pip install --user pre-commit

  c. Via ``pipx`` tool:

     .. code-block:: console

         pipx install pre-commit

2. Then generate git pre-commit hooks:

  .. code-block:: console

      pre-commit install

You may run pre-commit manually on all tracked files by calling:

.. code-block:: console

    pre-commit run --all-files


Tips
----

To run a subset of tests:

.. code-block:: console

    pytest tests.test_ansible_rulebook



To run E2E tests

.. code-block:: console

    pytest -m e2e


Building
---------

.. code-block:: console

    python -m build
    twine upload dist/*

Releasing
---------


.. code-block:: console

    bump2version patch # possible: major / minor / patch
    git push
    git push --tags




