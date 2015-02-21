Command line
============

floto supports several entry points depending on the context.
The easiest way is to use gradle to download the floto binaries and run them.

Common command line arguments
-----------------------------

The following common command line arguments are supported:

.. option:: --root <rootfile>

   The root system definition file (site JS)

.. option:: --environment <environment>
  
   The target environment (e.g. production, development, testing)

.. option:: --no-proxy

   Disable the embedded HTTP proxy used to cache and speed up downloads

.. option:: --proxy-url <proxyurl>

   Set an external HTTP-proxy address to use for downloads

FlotoServer
-----------

The server (io.github.floto.server.FlotoServer) can be used to start the web interface.
This interface allows a convenient way of redeploying, starting and stopping containers.

.. option:: --dev, --development-mode

   Start in development mode.
   This makes using floto better suited during development.
   Specifically:
    * The default deployment mode is from root image instead of from base image, making it easier to pick up definition changes.
    * The safety switch in the UI is toggled off by default.
    

.. option:: --port <port>

   Use the given port instead of the default of 40004.

FlotoBuilder
------------

The builder (io.github.floto.builder.FlotoBuilder) can be used to create standalone images.
This programm is run headless and produces a complete image with installed and configured containers.

As of now, the builder has no additional parameters.