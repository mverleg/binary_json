
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



Object interning
+++++++++++++++++++++++++++++++



Homogeneous N-dimensional arrays
+++++++++++++++++++++++++++++++++



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
.. _`the format description`: https://github.com/mverleg/vinary_json/blob/master/storage_format.rst
.. _`Revised BSD License`: https://github.com/mverleg/vinary_json/blob/master/LICENSE.rst
.. _JVM: https://github.com/mverleg/vinary_json/blob/master/kotlin/README_JVM.rst
.. _Kotlin: https://github.com/mverleg/vinary_json/blob/master/kotlin/
.. _Binary: https://github.com/mverleg/vinary_json/blob/master/rust/
.. _Rust: https://github.com/mverleg/vinary_json/blob/master/rust/
.. _Python: https://github.com/mverleg/vinary_json/blob/master/python/
.. _Javascript: https://github.com/mverleg/vinary_json/blob/master/kotlin/README_JS.rst


