+++
title = "Using the 3DConnexion mouse with a Qt Application"
slug = "2011-02-05-using-the-3dconnexion-mouse-with-a-qt-application"
published = 2011-02-05T20:03:00.002000+09:00
author = "David Dibben"
tags = []
+++
This note describes my experiences getting a 3D mouse to work in a Qt
application on Windows.  
  
The [3DConnexion](http://www.3dconnexion.com/) 3D mouse is a 6-DOF
controller often used for CAD and engineering applications. 3DConnexion
provide an SDK for windows which provides integration with MFC
applications but not for Qt.  
  
  
**RAWINPUT support for Qt**  
  
The recommended method of supporting the 3DConnexion 3D mouse is to
use Windows RAWINPUT message to receive the data from the mouse and then
process those message to get the motion data.  
  
There are 2 problems here  
  

-   Qt has no native support for RAWINPUT - it is a windows only system
    and Qt has no corresponding Qt events for the 3D mouse
-   The "out-of-the-box" version of Qt does not forward RAWINPUT
    messages as they are received - at least up to Qt 4.6.2. <span
    class="underline">On windows 7 Qt4.7.1 seemed to work with no
    modification</span>.

  
The Raw Input API provides a "stable and robust way for applications
to accept raw input from any HID, including the keyboard and mouse."
\[[msdn](http://msdn.microsoft.com/en-us/library/ms645543(v=vs.85).aspx)\]
This enables the application to get the actual data sent by the HID
device without any processing being done by windows first.  
  
The application first registers to receive Raw Input from a
particular device type, then when that device has data the application
receives a WM\_INPUT message in its event queue and the queue status
flag <span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">QS\_RAWINPUT
</span>is set. The application can then retrieve the data using the Raw
Input API.  
  
Raw Input was added in Windows XP, so is not available in Windows 2000  
(Which is important -- see below.)  
  
**Raw Input and Qt**  
  
The problem with Qt (at least in 4.6.2) is that the version from the
installer does not process Raw Input messages correctly. The way of
collecting these the Raw Input messages is to set an event filter on the
QApplication which gets the native windows messages. These can then be
processed by the application using the Windows Raw Input API. However,
the WM\_INPUT messages are not being received by window/event filter the
until some other event such as a mouse or timer event occurrs. Moving
the 3D mouse causes no events to be received by the event filter but
then if the normal mouse is moved (or key pressed etc)  
all(?) the 3D mouse events arrive.  
  
The problem can be traced to QEventDispatcherWin32?, which maps the
windows messages onto Qt Events. Specifically, the line  
  
<span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">  
MsgWaitForMultipleObjectsEX(nCount, pHandles, INFINITE,
QS\_ALLINPUT,</span><span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">MWMO\_ALERTABLE);</span>  
  
in the processEvents function of QEventDispatcherWin32. This is
blocking and not waking on WM\_INPUT events.  
  
The windows documentation for this notes that <span
class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">QS\_ALLINPUT</span>,
which includes <span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">QS\_INPUT</span>,
“does not include <span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">QS\_RAWINPUT
</span>in Windows2000.” Therefore, the problem is that the binary Qt
installer is built to work on all windows platforms, so during the
compile <span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">\_WIN32\_WINNT
</span>is defined to something less  
that WinXP? (0×501) so that raw-input messages are not handled.  
  
The fix is to re-compile Qt passing <span class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">-D
\_WIN32\_WINNT=0×501</span> to configure so that the WM\_INPUT messages
are correctly passed to the event filter when the 3D mouse is moved.  
  
So this is not really a Qt bug, but rather that Qt is compiled for
an "earlier" Windows platform which does not support Raw Input.  
  
**Sample Code for Qt and the 3D Mouse**  
  
I updated the 3DConennexion code for MFC to work with Qt. It uses an
event filter to pick up the raw windows events then extracts the 3D
Mouse information. This is then available as a Qt <span
class="Apple-style-span"
style="font-family: 'Courier New', Courier, monospace;">signal</span>.  
  
The zip file below contains a very simple application which displays the
motion data in a window. This was tested with Qt 4.7.1.  
  
[3DMouse.zip](http://codegardening.s3.amazonaws.com/3DMouse.zip)
