===================
Regular Expressions
===================

**regex** = regular expression

Synthax
=======

=============== ======================================= =============== ============================================
Sign            Explanation                             Expression      String containing the expression
=============== ======================================= =============== ============================================
``^foo``        string beginning with 'foo'             ^foo            'foobar', 'foo'
``bar$``        string ending with 'bar'                bar$            'foobar', 'bar' 
``*``           0, 1 or more                            abc*            'ab', 'abc', 'abcc', 'abcccccc'
``+``           1 or more                               abc+            'abc', 'abcc', 'abccc'
``?``           0 or 1                                  abc?            'ab', 'abc'
``{n}``         n times 'c'                             abc{4}          'abcccc'
``{n,m}``       n to m times 'c'                        abc{2,4}        'abcc', abccc', abcccc'
``{,m}``        0 to m times 'c'                        abc{,4}         'ab', 'abc', 'abcc', abccc', abcccc'
``{n,}``        n or more times 'c'                     abc{,2}         'abcc', 'abccc', 'abcccc'
``[abcd]``      'a' or 'b' or 'c' or 'd'                abc[abcd]       'abca', 'abcb', 'abcc', 'abcd'
``[a-d]``       any char between 'a' and 'd'            abc[a-d]        'abca', 'abcb', 'abcc', 'abcd'
``[a-d]{n}``    n times any char btw 'a' and 'd'        abc[a-d]{2}     'abcab', 'abcbd', 'abccc', 'abcdd'
``(abc){n}``    n times the string 'abc'                abc(def){2}     'abcdefdef'

=============== ======================================= =============== ============================================

Using the ``re`` module
=======================

``import re``

Search in a string : ``search``
-------------------------------



    
