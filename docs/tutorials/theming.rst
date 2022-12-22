.. _theming:

Changing the appearance of Open edX
===================================

Installing a custom theme
-------------------------

Comprehensive theming is enabled by default, but only the default theme is compiled. `Indigo <https://github.com/overhangio/indigo>`__ is a better, ready-to-run theme that you can start using today.

To compile your own theme, add it to the ``env/build/openedx/themes/`` folder::

    git clone https://github.com/me/myopenedxtheme.git \
      "$(tutor config printroot)/env/build/openedx/themes/myopenedxtheme"

The ``themes`` folder should have the following structure::

    openedx/themes/
        mycustomtheme1/
            cms/
                ...
            lms/
                ...
        mycustomtheme2/
            ...

Then you must rebuild the openedx Docker image::

    tutor images build openedx

Finally, you should enable your theme with the :ref:`settheme command <settheme>`.
