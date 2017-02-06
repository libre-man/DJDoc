Inner workings
===============
The app allows users to join your silent disco sessions and manage their personal information that is stored. In addition it logs data to the server to improve picking new songs and for (perhaps) research purposes.

Streaming music
---------------
The app's main purpose is playing music streamed by our server. With a silent disco, it is of key importance that all music played on all clients (apps) is played as closely to perfectly synchronous as possible. Minor delays between music played on clients can already have a huge impact. To make sure all clients are *in sync*, the ``NTP`` (= ``Network Time Protocol``) is used.

Logging data
------------
Another important aspect of the app is the ability to log data back to the server. This data is then used to constantly improve the selection of upcoming songs. It can also be used for research purposes. Right now, both channel switches and movement can be logged to the server. However only channel switches are used as feedback to improve the selection of new music. Thus right now only channel switches are actually sent to the server.

It is however easy to add new data to log. Data logging is done asynchronously in the ``Logger.java`` class. If one wants to add movement (measured via the accelerometer) to log, the ``onSensorChanged`` function can be uncommented and added to the data logging in the ``intervalLogger``. If one wants to log other data (e.g. position) this can also be done in this class.
