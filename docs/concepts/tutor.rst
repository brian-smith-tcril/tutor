.. _tutor_concepts:

Tutor
=====

What is Tutor?
--------------

Tutor is an open source distribution of `Open edX <https://open.edx.org>`_. It uses the original code from the various Open edX repositories, such as `edx-platform <https://github.com/openedx/edx-platform/>`_, `cs_comments_service <https://github.com/openedx/cs_comments_service>`_, etc. and packages everything in a way that makes it very easy to install, administer and upgrade Open edX. In particular, all services are run inside Docker containers.

Tutor makes it possible to deploy Open edX locally, with `docker-compose <https://docs.docker.com/compose/overview/>`_ or on an existing `Kubernetes cluster <http://kubernetes.io/>`_.

What is the purpose of Tutor?
-----------------------------

To make it possible to deploy, administer and upgrade Open edX anywhere, easily.

.. _how_does_tutor_work:

How does Tutor work?
--------------------

Tutor is a piece of software that takes care of exactly three things:

1. Project configuration: user-specific settings (such as secrets) are stored in a single ``config.yml`` file.
2. Template rendering: all the files that are necessary to run your platform are generated from a set of templates and user-specific settings.
3. Command-line interface (CLI): frequently-used administration commands are gathered in a convenient, unified CLI.

You can experiment with Tutor very quickly: start by :ref:`installing <install>` Tutor. Then run::

    $ tutor config save --interactive

Then, to view the result of the above command::

    $ cd "$(tutor config printroot)"
    $ ls
    config.yml  env

The ``config.yml`` file contains your user-specific Open edX settings (item #1 above). The ``env/`` folder contains the rendered templates which will be used to run your Open edX platform (item #2). For instance, the ``env/local`` folder contains the ``docker-compose.yml`` file to run Open edX locally.

The values from ``config.yml`` are used to generate the environment files in ``env/``. As a consequence, **every time the values from** ``config.yml`` **are modified, the environment must be regenerated** with ``tutor config save``..

Because the Tutor environment is generated entirely from the values in ``config.yml``, you can ``rm -rf`` the ``env/`` folder at any time and re-create it with ``tutor config save``. Another consequence is that **any manual change made to a file in** ``env/`` **will be overwritten by** ``tutor config save`` **commands**. Consider yourself warned!

You can now take advantage of the Tutor-powered CLI (item #3) to bootstrap your Open edX platform::

    tutor local launch

Under the hood, Tutor simply runs ``docker-compose`` and ``docker`` commands to launch your platform. These commands are printed in the standard output, such that you are free to replicate the same behaviour by simply copying/pasting the same commands.