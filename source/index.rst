.. Exosite Solutions Guide documentation master file, created by
   sphinx-quickstart on Fri Jul 24 12:44:12 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Exosite Solutions Guide's documentation!
===================================================

This guide is intended to give the user a quick introduction to building an IoT
solution based on the Exosite cloud.  This guide encompasses getting
data from your physical devices up to the Exosite OnePlatform.  For an introduction
on the front end portion of your solution, please see....

Gateway
    A device that has a connection to the Internet.  This connection can be WiFi,
    Ethernet, cellular, or any other link that allows it to talk to Exosite.  The
    gateway will also have a way to communicate with local nodes
Node
    A device that has data it needs to send to Exosite, but it doesn't 
    have its own connection to Exosite.  It therefore relays that data through
    a gateway.

Contents:

.. toctree::
   :maxdepth: 1
   
   gateway_design
   api_usage
   gateway_engine



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

