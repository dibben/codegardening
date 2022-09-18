+++
title = "Development environments for C++"
slug = "2010-07-04-development-environments-for-c"
published = 2010-07-04T12:45:00+09:00
author = "David Dibben"
tags = [ "Qt",]
+++
I have not been a big fan of IDEs. Several times I tried to get used to
Visual Studio but always found it big, slow and not suited to the way I
work. For a long time my development environment on Linux consisted of
multiple instances of Kate (a KDE text editor) each on a different
desktop and several small scripts. I would have source files in one
editor and headers in another, so when working on a single class a
simple keystroke to switch desktops would also switch header and source
files. An “edit” script would open the file in the right text editor
from the command line – I don’t think I ever used the file open dialog
to open a file. Searching across multiple files was done using the GNU
id-tools; very fast and easy to filter the output. As others have said,
UNIX is the IDE.  

  
Another requirement issupport for writing unit tests and Test Driven
Development. With multiple editors open, I can have the test code in one
editor and the source in another so switching is simple. A simple script
“tests” run from the command line, builds the source, builds the tests
and then runs the test cases.  Another script creates a new test
function. We use CppUnit for testing, which is OK but does need a lot of
boilerplate. Adding a new test requires not only the test function
itself but also a declaration in the header file and a registration
macro so the function is called by the test suite – this  is C++ so no
reflection to automatically pickup the test functions. Since the boiler
plate is always the same, except for the function name it is an ideal
candidate for a script:  
  

> <span style="font-size: small;">addtest  MyTestClass testFunctionOne
> testFunctionTwo testFunctionThree</span>

would add three new functions and their declarations to the test
class.  

So basically, I was happy with my development environment. But there
were two problems. I also have to develop on Windows and even with
cygwin the environment there always seemed slower and I had to use a
different editor. Secondly, all my colleagues use Windows with Visual
Studio.  I see them struggling with basic tasks; they ask for my help on
some coding problem so I suggest that they open a particular file and 2
minutes later they are still faffing around clicking through directories
in a file open dialog. The majority of this problem is probably their
knowledge of the environment rather than a problem with VS itself.  But,
Visual Studio does have some significant problems for our C++
development.  

We use Qt, which has its own project management system. The project is
defined in .pro files which are then converted into makefiles by qmake.
Visual Studio project files (vproj) files can also be made by qmake, so
when a project is updated, the visual studio build files need to updated
and then re-loaded. This means we don’t use Visual Studio’s project
management functions. Even if we didn’t have this restriction I don’t
like vproj files anyway because they are hard to manage in a version
control system because they are [difficult to
merge](http://stackoverflow.com/questions/166796/how-do-you-manage-vcproj-files-in-souce-control-which-are-changed-by-multiple-de).
The second problem with Visual Studio is that it has no specific support
for unit tests.

  

As a senior developer in the group I have some responsibility for the
tools that the other developers use.  They want to use a nice graphical
IDE – because it is easier. But I see all sorts of productivity problems
in the way that they use it. We have a large code base, use Qt for the
GUI and VisualStudio does not seem to handle this well at all.  

So what I wanted was a development environment suited to large C++ Qt
applications where I could use the same tools on Windows and Linux. It
should have enough graphical features to not frighten the junior
developers used to their cozy WIMP world but should have enough keyboard
shortcuts to allow efficient development and be customizable for our
specific requirements.  

Then Trolltech released
[Qt-Creator](http://qt.nokia.com/products/appdev/developer-tools/developer-tools#qt-tools-at-a). 
While clearly not as comprehensive as Visual Studio, it is specifically
targeted at the type of development that we are doing.  I have now
switched to Qt-Creator and the next post will be on my experiences so
far.
