##########
API Usage
##########
This is meant to be a high level primer on using Exosite's APIs.  For the full
API documentation, please see the official Exosite docs page (http://docs.exosite.com/).
Before reading this document, you should be familiar with HTTP.  If you're not
familiar, `this page <http://www.jmarshall.com/easy/http/>`_ gives a good introduction.

RPC, Data, or CoAP?
------------------------------
Exosite API calls can be made using 
the `Exosite JSON RPC interface <http://docs.exosite.com/rpc/>`_, 
the `Exosite Data Interface <http://docs.exosite.com/http/>`_, or 
the `Exosite CoAP Interface <http://docs.exosite.com/http/>`_.  Which API
you choose depends on the architeture of your gateway.

Data Interface
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

Read
""""
If you want to read from a datasource, you make a ``GET`` request to 
``GET /onep:v1/stack/alias?<alias 1>`` where ``<alias 1>`` is the name of your
devices datasource you want to read from. For example, if you want to read from
your device's ``temperature`` datasource, you would make a ``GET`` request to
``GET /onep:v1/stack/alias?temperature``, and the body of the response would
look like this: ``temperature=24``.  

.. note:: Your read responses will have the body 
 `url encoded <http://www.w3schools.com/tags/ref_urlencode.asp>`_
 
.. note:: If your requests has multiple aliases, they will be seperated by a
 ``\r\n`` in the body.

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

JSON RPC
~~~~~~~~
The JSON RPC uses commands encoded in as `JSON <http://www.w3schools.com/json/>`_.
Using the JSON RPC, you can send multiple commands at once, or 
The JSON RPC interface is Exosite's full featured API.  Using the JSON RPC, you
can perfor
