Google Noto Fonts Container
================================

This image provides the full set of Google Noto fonts (https://www.google.com/get/noto/) along with a simple
FOP configuration file that uses the fonts. The fonts take almost a gigabyte of space so it's useful to
have them in a separate container.

This container defines the following volumes:

~~~~
VOLUME /usr/share/fonts
VOLUME /opt/fop
~~~~

/usr/share/fonts/noto contains all the Noto fonts, /opt/fop contains fop.xconf, which configures the
font directory to FOP.
 