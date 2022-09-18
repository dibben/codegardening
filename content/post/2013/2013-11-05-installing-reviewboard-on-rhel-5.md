+++
title = "Installing ReviewBoard on RHEL-5"
slug = "2013-11-05-installing-reviewboard-on-rhel-5"
published = 2013-11-05T21:51:00.002000+09:00
author = "David Dibben"
tags = []
+++
[ReviewBoard](http://www.reviewboard.org/) is a great free code review
tool which we have been using for several years now. We run it on a
Redhat server and it is connected to our Subversion repository. With the
1.7 release of ReviewBoard support for Python 2.4 was dropped and
unfortunately that is the standard Python on RHEL-5. So I have been
putting off upgrading for some time.  
  
Finally decided to upgrade and switch from using the SQLite database to
MySQL. Since we have a small team we have not had any performance
problems with SQLite, except where the source code in a review is split
across multiple pages when changing the page with an open review causes
the DB to get locked and requiring a restart of Apache. The ReviewBoard
docs do warn about using SQLite but we have been using ReviewBoard since
before version 1 when the install process and DB support was not nearly
as good as it is now.  
  
So first task was to get a newer Python. Fortunately this turned out to
be much easier than expected since the Extra Packages for Enterprise
Linux ([EPEL](http://fedoraproject.org/wiki/EPEL)) contain the rpms for
Python 2.6 so it was as easy as  
  
<span style="font-family: Courier New, Courier, monospace;">    yum
install python26</span>  
  
Now installing ReviewBoard should be extremely easy. On my Fedora box at
home, I could just type  
  
<span style="font-family: Courier New, Courier, monospace;">   
easy\_install ReviewBoard</span>  
  
and ReviewBoard and all its dependencies were installed. Trivially easy.
Unfortunately the server is behind a proxy server. Setting the
http\_proxy environment variable and the values in yum.comf were enough
to get yum to work, but not easy\_install. That kept on giving errors.  
  
After several frustrating hours trying to different proxy server
settings I eventually stumbled on the solution: Our proxy server seems
to require that http<span style="color: red;">s</span>\_proxy is set in
addition to  http\_proxy. So setting both:  
  
<span style="font-family: Courier New, Courier, monospace;">   export
http\_proxy=http://192.168.1.1:80</span>  
<span style="font-family: Courier New, Courier, monospace;">   export
https\_proxy=http://192.168.1.1:80</span>  
  
and it installed!  The Google search for easy\_install proxy problems
never mentioned this. So I don't know whether this is an easy\_install
problem or our peculiar proxy server.  
  
Of course, it still wasn't that easy. While setting up the site MySQL
was not available because the install of the pymysql had failed because
the MySQL devel package was not installed and there was no error message
visible during the easy\_install.  
  
However, finally it works. Unfortunately, there is no easy way to
migrate the old SQLite data to MySQL.  
  

[![](../images/thumbnails/2013-11-05-installing-reviewboard-on-rhel-5-reviewboard-1.png)](../images/2013-11-05-installing-reviewboard-on-rhel-5-reviewboard-1.png)
