+++
title = "Windows SDK Woes"
slug = "2011-12-29-windows-sdk-woes"
published = 2011-12-29T10:00:00+09:00
author = "David Dibben"
tags = []
+++
Finally got a Windows 7 PC at work. Installing the Microsoft Platform
SDK kept on failing with a not too helpful error message.  
  
  
<span
style="background-color: white; color: #2a2a2a; font-family: Calibri, sans-serif; font-size: 15px; line-height: 17px; text-align: left;">Installation
of the "Microsoft Windows SDK for Windows 7" product has reported the
following error: Please refer to Samples\\Setup\\HTML\\ConfigDetails.htm
document for further information.</span>  

  

The log file is not too helpful as it contains many errors, but most of
them seem to be spurious.

  

  
It seems that if a more recent version of the "Visual C++ 2010 x86
Redistributable" (vcredist\_x64.exe) is installed then the SDK install
fails. The
[solution](http://social.msdn.microsoft.com/Forums/en-US/windowssdk/thread/8f3350f9-0b47-40ae-b070-f2ccbf041875/)
is to first unistall the redistributable package then install the SDK.  
  
Since the redistributables are updated with windows update I expect that
this is a common problem. MS could at least put a note on the download
page for the SDK about this.
