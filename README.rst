Introduction
============

.. image:: https://readthedocs.org/projects/adafruit-circuitpython-il91874/badge/?version=latest
    :target: https://circuitpython.readthedocs.io/projects/il91874/en/latest/
    :alt: Documentation Status

.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://discord.gg/nBQh6qu
    :alt: Discord

.. image:: https://github.com/adafruit/Adafruit_CircuitPython_IL91874/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_IL91874/actions
    :alt: Build Status

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
    python3 -m venv .env
    source .env/bin/activate
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
    import adafruit_il91874

    displayio.release_displays()

    spi = board.SPI()
    epd_cs = board.D10
    epd_dc = board.D9

    display_bus = displayio.FourWire(spi, command=epd_dc, chip_select=epd_cs, baudrate=1000000)
    time.sleep(1)

    display = adafruit_il91874.IL91874(display_bus, width=264, height=176, highlight_color=0xff0000, rotation=90)

    g = displayio.Group()

    f = open("/display-ruler.bmp", "rb")

    pic = displayio.OnDiskBitmap(f)
    t = displayio.TileGrid(pic, pixel_shader=displayio.ColorConverter())
    g.append(t)

    display.show(g)

    display.refresh()

    print("refreshed")

    time.sleep(120)

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_IL91874/blob/master/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Documentation
=============

For information on building library documentation, please check out `this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.
