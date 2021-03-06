JMESPath
========


.. image:: https://badges.gitter.im/Join Chat.svg
   :target: https://gitter.im/jmespath/chat


.. image:: https://secure.travis-ci.org/jmespath/jmespath.py.png?branch=develop
   :target: http://travis-ci.org/jmespath/jmespath.py


JMESPath (pronounced "james path") allows you to declaratively specify how to
extract elements from a JSON document.

For example, given this document::

    {"foo": {"bar": "baz"}}

The jmespath expression ``foo.bar`` will return "baz".

JMESPath also supports:

Referencing elements in a list.  Given the data::

    {"foo": {"bar": ["one", "two"]}}

The expression: ``foo.bar[0]`` will return "one".
You can also reference all the items in a list using the ``*``
syntax::

   {"foo": {"bar": [{"name": "one"}, {"name": "two"}]}}

The expression: ``foo.bar[*].name`` will return ["one", "two"].
Negative indexing is also supported (-1 refers to the last element
in the list).  Given the data above, the expression
``foo.bar[-1].name`` will return "two".

The ``*`` can also be used for hash types::

   {"foo": {"bar": {"name": "one"}, "baz": {"name": "two"}}}

The expression: ``foo.*.name`` will return ["one", "two"].


API
===

The ``jmespath.py`` library has two functions
that operate on python data structures.  You can use ``search``
and give it the jmespath expression and the data::

    >>> import jmespath
    >>> path = jmespath.search('foo.bar', {'foo': {'bar': 'baz'}})
    'baz'

Similar to the ``re`` module, you can use the ``compile`` function
to compile the JMESPath expression and use this parsed expression
to perform repeated searches::

    >>> import jmespath
    >>> expression = jmespath.compile('foo.bar')
    >>> expression.search({'foo': {'bar': 'baz'}})
    'baz'
    >>> expression.search({'foo': {'bar': 'other'}})
    'other'

This is useful if you're going to use the same jmespath expression to
search multiple documents.  This avoids having to reparse the
JMESPath expression each time you search a new document.


Specification
=============

If you'd like to learn more about the JMESPath language, you can check out
the `JMESPath tutorial <http://jmespath.org/tutorial.html>`__.  Also check
out the `JMESPath examples page <http://jmespath.org/examples.html>`__ for
examples of more complex jmespath queries.

The grammar is specified using ABNF, as described in
`RFC4234 <http://www.ietf.org/rfc/rfc4234.txt>`_.
You can find the most up to date
`grammar for JMESPath here <http://jmespath.org/specification.html#grammar>`__.

You can read the full
`JMESPath specification here <http://jmespath.org/specification.html>`__.


Testing
=======

In addition to the unit tests for the jmespath modules,
there is a ``tests/compliance`` directory that contains
.json files with test cases.  This allows other implementations
to verify they are producing the correct output.  Each json
file is grouped by feature.


Discuss
=======

Join us on our `Gitter channel <https://gitter.im/jmespath/chat>`__
if you want to chat or if you have any questions.
