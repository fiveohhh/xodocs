##########
API Usage
##########
This is meant to be a high level primer on using Exosite's APIs.  For the full
API documentation, please see the official Exosite docs page (http://docs.exosite.com/).
Before reading this document, you should be familiar with HTTP.  If you're not
familiar, `this page <http://www.jmarshall.com/easy/http/>`_ gives a good introduction.

This page does not cover the device provisioning process for details on the
API's required to provision your device, please see the :doc:`provisioning` doc.

Data, RPC, or CoAP?
------------------------------
Exosite API calls can be made using 
the `Exosite Data Interface <http://docs.exosite.com/http/>`_,
the `Exosite JSON RPC interface <http://docs.exosite.com/rpc/>`_, or 
the `Exosite CoAP Interface <http://docs.exosite.com/http/>`_.  Which API
you choose depends on the architeture of your gateway.

Data API
~~~~~~~~~~~~~~
The Data API is a simple API built on top of HTTP. It uses HTTP and provides
the following basic functions.

* `Write <http://docs.exosite.com/http/#write>`_
* `Read <http://docs.exosite.com/http/#read>`_
* `Read/Write <http://docs.exosite.com/http/#hybrid-readwrite>`_
* `Long-Polling <http://docs.exosite.com/http/#long-polling>`_

Write
"""""
If you want to write the value ``24`` to your devices ``temperature`` 
datasource, the body of your ``POST`` request is simply ``temperature=24``.  

Data API Example:

.. code-block:: http

    POST /onep:v1/stack/alias HTTP/1.1 
    Host: m2.exosite.com 
    X-Exosite-CIK: < your cik >
    Content-Type: application/x-www-form-urlencoded; charset=utf-8 
    Content-Length: 14
    
    temperature=24

Read
""""
If you want to read from a datasource, you make a ``GET`` request to 
``GET /onep:v1/stack/alias?<alias 1>`` where ``<alias 1>`` is the name of your
devices datasource you want to read from. For example, if you want to read from
your device's ``temperature`` datasource, you would make a ``GET`` request to
``GET /onep:v1/stack/alias?temperature``, and the body of the response would
look like this: ``temperature=24``.  

Data API Example:

.. code-block:: http

    GET /onep:v1/stack/alias?temperature HTTP/1.1 
    Host: m2.exosite.com 
    X-Exosite-CIK: < your cik >
    Content-Type: application/x-www-form-urlencoded; charset=utf-8 
    Content-Length: 0


.. note:: Your read responses will have the body 
 `url encoded <http://www.w3schools.com/tags/ref_urlencode.asp>`_
 
.. note:: With the data API, if your requests has multiple aliases, they will 
 be seperated by a ``\r\n`` in the body.

If you want to read from multiple datasources at the same time, you would add
multiple datasources as URL parameters and seperate them with an ``&`` 
(e.g. ``/onep:v1/stack/alias?temperature&humidity``).  The response would contain
your read values seperated by an ``&`` (e.g. temperature=25&humidity=77).
 
Read/Write
""""""""""
The read/write command allows you to perform a read and a write request at the
same time.  To do this, you combine both of the above methods and make a ``POST``
request to ``/onep:v1/stack/alias?<alias 1>`` while also including your write
values in the body of your request.  The response of your request will contain
the values of your read requests.

Data API Example:

.. code-block:: http

    POST /onep:v1/stack/alias?temperature HTTP/1.1 
    Host: m2.exosite.com 
    X-Exosite-CIK: < your cik >
    Content-Type: application/x-www-form-urlencoded; charset=utf-8 
    Content-Length: 14
    
    temperature=24

JSON RPC
~~~~~~~~
The JSON RPC uses commands encoded in as `JSON <http://www.w3schools.com/json/>`_.
Using the JSON RPC, you can send multiple commands at once.  It provides the most
features of any of Exosite's APIs.

The main disadvantage to using the JSON RPC is that it requires the most bandwidth
and it also requires the application to parse/build json.  Most higher level
languages have support for this.  If you are developing in C, Exosite has
successfully used the Jsmn library for parsing JSON.  For more details on using
Jsmn in your project, please see the `Jsmn development guide <>`_.

Here is a full list of the JSON RPC commands.  We will cover a small subset of
the commands that allow your device to read/write data to Exosite.

CoAP
~~~~
The CoAP API is intended to be used for low bandwidth devices.

DTLS
""""
The CoAP API also has the ability to use a form of DTLS to keep the link between
Exosite and your device private.