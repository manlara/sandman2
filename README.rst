sandman2
========

sandman2 automagically generates RESTful APIs for existing databases.
Why is that useful? Imagine you're working for AnonymousCorp and need to
access Group Y's data, which is presented to you through some horrible
API or GUI. Wouldn't it be nice if you could just interact with that
database through a REST API?

More than that, imagine if you could interact with the database through
a REST API **and no one had to write any code**. No boilerplate ORM
code, no database connection logic. Nothing. sandman2 can be run as a
command-line tool (``sandman2ctl``) that just takes your database
information as parameters and connects to it, introspects the schema,
generates a RESTful API, and starts the server.

What Happened to Sandman (1)?
-----------------------------

```sandman`` <http://www.github.com/jeffknupp/sandman>`__, the precursor
to ``sandman2``, is no longer being maintianed. ``sandman`` had almost
identical functionality but had an architecutre that reflected the
capabilities of the underlying ORM, SQLAlchemy. As of the ``0.9``
release, SQLAlchemy introduced the ``automap`` construct. This
fundamentally changed the way that ``sandman`` *could* interact with the
underlying database in a way that greatly simplified things. All that
was needed was the actual effort to rewrite ``sandman`` from scratch...

After wrestling with the idea for a while, I finally gave in and started
the rewrite project. ``sandman2`` is that project. While I'll continue
to support ``sandman`` in the nearterm, ``sandman2`` definitely
represents the way forward.

Quickstart
----------

Install sandman2 using ``pip``: ``$ pip install sandman2``. This
provides the script ``sandman2ctl``, which just takes the database URI
string, described
`here <http://docs.sqlalchemy.org/en/rel_0_9/core/engines.html>`__. For
example, to connect to a SQLite database in the same directory you're
running the script, you would run:

.. code:: bash

    $ sandman2ctl sqlite+pysqlite:///database_file_name

To connect to a PostgreSQL database, make sure you install a driver like
``psycopg2`` using ``pip``, then use the following connection string:

.. code:: bash

    $ sandman2ctl postgresql+psycopg2://scott:tiger@localhost/mydatabase

Again, see `the SQLAlchemy
documentation <http://docs.sqlalchemy.org/en/rel_0_9/core/engines.html>`__
for a more comprehensive discussion of connection strings.

Supported Databases
-------------------

sandman2 supports all databases that the underlying ORM, SQLAlchemy,
supports. Presently, that includes:

-  MySQL
-  PostgreSQL
-  Oracle
-  Microsoft SQL Server
-  SQLite
-  Sybase
-  Drizzle
-  Firebird

Third-party packages extend support to:

-  IBM DB2
-  Amazon Redshift
-  SQL Anywhere
-  MonetDB

Admin Interface
---------------

One of the best things about the original
`sandman <http://www.github.com/jeffknupp/sandman>`__ was the *Admin
Interface*. Not only does sandman2 include the Admin Interface, but it
modernize's it as well. The layout has been greatly improved, especially
when dealing with more than about eight tables. All of the original
functionality of the Admin Interface remains unchanged.

Here's a shot of the new look:

.. figure:: http://sandman.io/static/img/sandman2-admin.png
   :alt: admin interface awesomesauce screenshot

   admin interface awesomesauce screenshot
Customizing
-----------

If ``sandman2ctl`` doesn't give you fine-grained enough control over
your REST endpoints, or you'd like to restrict the set of tables made
available via ``sandman2ctl``, you can easily integrate ``sandman2``
into your application. See the documentation for more info.