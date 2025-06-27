Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-il91874/badge/?version=latest
    :target: https://docs.circuitpython.org/projects/il91874/en/latest/
    :alt: Documentation Status

.. image:: https://raw.githubusercontent.com/adafruit/Adafruit_CircuitPython_Bundle/main/badges/adafruit_discord.svg
    :target: https://adafru.it/discord
    :alt: Discord

.. image:: https://github.com/adafruit/Adafruit_CircuitPython_IL91874/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_IL91874/actions
    :alt: Build Status

.. image:: https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json
    :target: https://github.com/astral-sh/ruff
    :alt: Code Style: Ruff

CircuitPython `displayio` driver for IL91874-based ePaper displays


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://github.com/adafruit/Adafruit_CircuitPython_Bundle>`_.

Installing from PyPI
=====================

On supported GNU/Linux systems like the Raspberry Pi, you can install the driver locally `from
PyPI <https://pypi.org/project/adafruit-circuitpython-il91874/>`_. To install for current user:

.. code-block:: shell

    pip3 install adafruit-circuitpython-il91874

To install system-wide (this may be required in some cases):

.. code-block:: shell

    sudo pip3 install adafruit-circuitpython-il91874

To install in a virtual environment in your current project:

.. code-block:: shell

    mkdir project-name && cd project-name
    python3 -m venv .venv
    source .venv/bin/activate
    pip3 install adafruit-circuitpython-il91874

Usage Example
=============

.. code-block:: python

    """Simple test script for 2.7" 264x176 Tri-Color display shield

    Supported products:
      * Adafruit 2.7" Tri-Color ePaper Display Shield
        * https://www.adafruit.com/product/4229
      """

    import time
    import board
    import busio
    import displayio
    import fourwire
    import adafruit_il91874

    displayio.release_displays()

    spi = board.SPI()
    epd_cs = board.D10
    epd_dc = board.D9

    display_bus = fourwire.FourWire(spi, command=epd_dc, chip_select=epd_cs, baudrate=1000000)
    time.sleep(1)

    display = adafruit_il91874.IL91874(display_bus, width=264, height=176, highlight_color=0xff0000, rotation=90)

    g = displayio.Group()

    pic = displayio.OnDiskBitmap("/display-ruler.bmp")
    # Create a Tilegrid with the bitmap and put in the displayio group
    t = displayio.TileGrid(pic, pixel_shader=pic.pixel_shader)
    g.append(t)

    # Place the display group on the screen (does not refresh)
    display.root_group = g

    # Show the image on the display
    display.refresh()

    print("refreshed")

    # Do Not refresh the screen more often than every 180 seconds
    #   for eInk displays! Rapid refreshes will damage the panel.
    time.sleep(180)


Documentation
=============

API documentation for this library can be found on `Read the Docs <https://docs.circuitpython.org/projects/il91874/en/latest/>`_.

For information on building library documentation, please check out `this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_IL91874/blob/main/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.
