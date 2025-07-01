Introduction
============


.. image:: https://readthedocs.org/projects/adafruit-circuitpython-color-terminal/badge/?version=latest
    :target: https://docs.circuitpython.org/projects/color_terminal/en/latest/
    :alt: Documentation Status


.. image:: https://raw.githubusercontent.com/adafruit/Adafruit_CircuitPython_Bundle/main/badges/adafruit_discord.svg
    :target: https://adafru.it/discord
    :alt: Discord


.. image:: https://github.com/adafruit/Adafruit_CircuitPython_Color_Terminal/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_Color_Terminal/actions
    :alt: Build Status


.. image:: https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json
    :target: https://github.com/astral-sh/ruff
    :alt: Code Style: Ruff

Extension of supports ANSI color escapes for subsets of text


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_
or individual libraries can be installed using
`circup <https://github.com/adafruit/circup>`_.


Installing from PyPI
=====================

On supported GNU/Linux systems like the Raspberry Pi, you can install the driver locally `from
PyPI <https://pypi.org/project/adafruit-circuitpython-color-terminal/>`_.
To install for current user:

.. code-block:: shell

    pip3 install adafruit-circuitpython-color-terminal

To install system-wide (this may be required in some cases):

.. code-block:: shell

    sudo pip3 install adafruit-circuitpython-color-terminal

To install in a virtual environment in your current project:

.. code-block:: shell

    mkdir project-name && cd project-name
    python3 -m venv .venv
    source .env/bin/activate
    pip3 install adafruit-circuitpython-color-terminal

Installing to a Connected CircuitPython Device with Circup
==========================================================

Make sure that you have ``circup`` installed in your Python environment.
Install it with the following command if necessary:

.. code-block:: shell

    pip3 install circup

With ``circup`` installed and your CircuitPython device connected use the
following command to install:

.. code-block:: shell

    circup install adafruit_color_terminal

Or the following command to update an existing version:

.. code-block:: shell

    circup update

Usage Example
=============

.. code-block:: python

    import supervisor
    from displayio import Group
    from terminalio import FONT

    from adafruit_color_terminal import ColorTerminal

    main_group = Group()
    display = supervisor.runtime.display
    font_bb = FONT.get_bounding_box()
    screen_size = (display.width // font_bb[0], display.height // font_bb[1])

    terminal = ColorTerminal(FONT, screen_size[0], screen_size[1])
    main_group.append(terminal.tilegrid)

    black = chr(27) + "[30m"
    red = chr(27) + "[31m"
    green = chr(27) + "[32m"
    yellow = chr(27) + "[33m"
    blue = chr(27) + "[34m"
    magenta = chr(27) + "[35m"
    cyan = chr(27) + "[36m"
    white = chr(27) + "[37m"
    reset = chr(27) + "[0m"


    message = f"Hello {green}World{reset} {yellow}ANSI\n"
    terminal.write(message)
    print(message, end="")

    message = f"{magenta}Terminal {red}Colors{reset}"
    terminal.write(message)
    print(message)

    display.root_group = main_group

    print(terminal.cursor_x, terminal.cursor_y)

    move_cursor = chr(27) + "[10;10H"
    terminal.write(f" Something {move_cursor}{cyan} Else{reset}")
    print(f" Something {move_cursor}{cyan} Else{reset}")

    while True:
        pass


Documentation
=============
API documentation for this library can be found on `Read the Docs <https://docs.circuitpython.org/projects/color_terminal/en/latest/>`_.

For information on building library documentation, please check out
`this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_Color_Terminal/blob/HEAD/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.
