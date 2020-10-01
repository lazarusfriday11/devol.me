.. meta::
    :title: Read Me

How to invoke python environment:
=================================

::
    source py_env/bin/activate

Source: https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-programming-environment-on-an-ubuntu-20-04-server

Ablog
=====


This site is built for use with `Ablog <https://ablog.readthedocs.io/>`__.

Basics
------


* Do not use a sphinx builder or ``make html``, instead use ``ablog build`` to perform the same function and utilize the features from ABlog.


* To make a blog post with ablog, use the ``.. post::`` directive:

    ::

        .. post:: Apr 15, 2014
            :tags: earth, love, peace
            :category: python
            :author: me
            :location: SF
            :language: en

* To show a list of posts (like from a category or year archive) use the ``.. postlist::`` directive:

    ::

       .. postlist::
          :list-style: circle
          :category: Manual
          :format: {title}
          :sort:



