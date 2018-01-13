
Binary JSON
===============================

This package encodes JSON-compatible data into a compact binary format.

It saves substantial amounts of space compared to plain-text and even compressed plain-text format, but it is not human-readable.

Status
-------------------------------

**This project is under development and is not yet ready to be used!**

Installation
-------------------------------

To use this library, please follow the steps for the platform(s) you use:

* JVM_ (Kotlin/Java/Scala/...)
* Javascript_ (browsers, Node)
* Binary_ (Rust/C/C++/C#/...)
* Python_

Advantages
-------------------------------

Compression
+++++++++++++++++++++++++++++++

By using a binary representation as well as several extra 'tricks' to avoid repetition, this format saves quite some space when storing or sending JSON data.

Disadvantages
-------------------------------

Not human readable
+++++++++++++++++++++++++++++++

One of the virtues of JSON is that it's easy to read by humans. For most humans, this is not the case for compressed, binary json.

However, JSON is also commonly used to communicate between computers or for storage. In those cases, this package can decrease the size of the data substantially.

Unsized / not seekable
+++++++++++++++++++++++++++++++

Unlike BSON_, this package does not implement a seekable format, but focuses instead of compression.

This means that (like normal JSON) there is no special way to quickly get a certain part of the data, without reading everything that comes before it.

Read/write speed
+++++++++++++++++++++++++++++++

TODO

Features
-------------------------------

String interning
+++++++++++++++++++++++++++++++

Each unique string is only stored once. Further occurrences refer to the stored version.

This happens automatically during encoding and decoding; you will not have to think about it.

Object interning
+++++++++++++++++++++++++++++++

This idea is still `under consideration`_; input is welcome.

The structure of objects is stored once; this means the keys, order and the types of values are stored, and each occurrence only stores the actual values without type information.

Consider e.g. these two objects::

    [{
        "name": "John Bardeen",
        "age": 82,
        "nobel_prizes": [
            ["physics", 1956],
            ["physics", 1972]
        ]
    },
    {
        "name": "M Verleg",
        "age": 29,
        "nobel_prizes": []
    }]

Both person-objects have the same structure, so the structure will be saved ones, abstractly something like this::

    #1: {
        "name": string,
        "age": int,
        "nobel_prizes": list
    }

and then the people can abstractly be stored as::

    [#1: "John Bardeen", 82, [["physics", 1956], ["physics", 1972]],
    [#1: "M Verleg", 29, [],

This happens automatically during encoding and decoding; you will not have to think about it.

Homogeneous N-dimensional arrays
+++++++++++++++++++++++++++++++++

Normal JSON is rather terrible at storing large amounts of homogeneous data, such as matrices; that is not what it was designed for.

However, this package is rather good at homogeneous matrices, which are stored not only as binary, but also without repeating type information, and with bytes aligned and possibly truncated for further compression.

No integer overflows
+++++++++++++++++++++++++++++++

This package uses `flex size ints`_, which both leads to compression of small integers and allows for integers to grow arbitrarily large.

Multi-platform
+++++++++++++++++++++++++++++++

This is not actually done yet, but the plan is to support multiple compatible versions:

- JVM_ (Kotlin_) (callable from JVM languages like Kotlin, Java, Scala)
- Javascript_ (Kotlin_) (usable in browsers and on Node)
- Rust_ (callable from Rust, C, C++, C#, Julia...)
- Python_ (callable from, well, Python)

This means you can save a compressed json file in Java and read it in C++, for example.

How does it work?
-------------------------------

For info about the storage format, see `the format description`_.

Usage & contributions
---------------------------------------

Code is under `Revised BSD License`_ so you can use it for most purposes including commercially.

After the code reaches a functional stage in Python, contributions are very welcome!

Tests
---------------------------------------

The project has good automated test coverage. Tests are run automatically for commits to the repository for all supported versions. This is the status:

.. image:: https://travis-ci.org/mverleg/binary_json.svg?branch=master
	:target: https://travis-ci.org/mverleg/binary_json


.. _BSON: http://bsonspec.org/
.. _`under consideration`: https://github.com/mverleg/binary_json/issues/2
.. _`the format description`: https://github.com/mverleg/vinary_json/blob/master/storage_format.rst
.. _`Revised BSD License`: https://github.com/mverleg/vinary_json/blob/master/LICENSE.rst
.. _JVM: https://github.com/mverleg/vinary_json/blob/master/kotlin/README_JVM.rst
.. _Kotlin: https://github.com/mverleg/vinary_json/blob/master/kotlin/
.. _Binary: https://github.com/mverleg/vinary_json/blob/master/rust/
.. _Rust: https://github.com/mverleg/vinary_json/blob/master/rust/
.. _Python: https://github.com/mverleg/vinary_json/blob/master/python/
.. _Javascript: https://github.com/mverleg/vinary_json/blob/master/kotlin/README_JS.rst
.. _`flex size ints`: https://github.com/mverleg/flex_size_int


