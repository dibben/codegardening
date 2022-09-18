+++
title = "A script for adding test cases to a CppUnit test class"
slug = "2010-07-09-a-script-for-adding-test-cases-to-a-cppunit-test-class"
published = 2010-07-09T22:15:00+09:00
author = "David Dibben"
tags = []
+++
One of the problems with using CppUnit as the unit test framwork in C++
is that adding a single test requires updating the code in two files and
in total 3 places. A declaration in the header file, a macro in the
header file to regsiter the test and the test itself. This makes adding
a test too hard, which means the tests themselves become too big because
it is easier to add extra asserts to an existing test than to add a new
test. Some of the newer C++ frameworks overcome this, but we have been
using CppUnit for a long time and have a lot of tests already written so
I do not really want to change frameworks.  
  
To fix this I created a small Python script to add a new test, so
working from the command line, I just need to write  

    newtest TestCase testMyNewTest

and the declaration and prototype are created. I don't need to even look
at the header file I can just go straight to the definition of the test
function and add the test.  
  
The header file for a CppUnit test case looks like this:  
  

    class TestCase : public CppUnit::TestFixture

    {

    CPPUNIT_TEST_SUITE( TestCase );

        CPPUNIT_TEST( testSomething );

        CPPUNIT_TEST( testNextBit );

      CPPUNIT_TEST_SUITE_END();

    public:

        void    setUp();
        void    tearDown();

     

<span style="color: silver;"></span>  

        void    testSomething();

        void    testNextBit();

    };

  
And the source file  
  

    CPPUNIT_TEST_SUITE_REGISTRATION( TestCase );

     

<span style="color: olive;"></span>  

    void TestCase::testSomething()

    {

     // test code here

    }

     

    void TestCase::testNextBit()

    {

     // test code here

    }

  
The script is very simple, it searches for the last CPPUNIT\_TEST macro
in the header and adds a macro for the new test case. Searchs for the
last test function, and adds a test after that. Then it adds a defintion
at the end of the source file.  
  
The script makes two assumptions  

-   The name of the class matches the name of the file. So the above
    test class would be in TestCase.h and TestCase.cpp
-   The test class already has at least one test function when the
    script is run. Since I use a separate script to generate the
    boilerplate test class with a single test this is always true in my
    case.

  
The script is available here in case it is of use to anyone else:
[newtest.py](http://codegardening.s3.amazonaws.com/newtest.py)
