+++
title = "Visual Studio 2012 breaks VS2010"
slug = "2012-09-15-visual-studio-2012-breaks-vs2010"
published = 2012-09-15T21:10:00.001000+09:00
author = "David Dibben"
tags = []
+++
[StackOverflow](http://stackoverflow.com/questions/10888391/link-fatal-error-lnk1123-failure-during-conversion-to-coff-file-invalid-or-c)
just rescued me again from yet another Microsoft problem. It seems if
you try to install Visual Studio 2012 when you already have a Visual
Studio 2010 installation then the 2010 installation gets broken.  
  
Fortunately MS have released a SP to 2010 which fixes the problem. But
it should not happen in the first place. Unless you do everything on a
virtual machine when you try a new program like VS2012 you will want to
keep your existing environment working. Did they not test installing
VS2012 onto a machine with VS2010? I can't believe that they did not,
which means that they must not care about breaking existing
environments.  There was no warning message that it would happen and the
Update for 2010 was only available after installing 2012.
