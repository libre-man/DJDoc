============
Android App
============
The app allows users to join your organized silent disco session. The app can be installed on any Android smartphone running ``Android 5.0 Lollipop`` (API 21) or higher and can be downloaded from `app.sdaas.nl <app.sdaas.nl>`_. The following section will explain how to use the app and briefly go over inner workings of it.

Using the app
--------------
.. image:: images/initial.jpg
   :height: 300px
   :align: right

When initially launching the app, it will prompt a settings screen asking for basic information. This will only be seen when starting the app for the first time. Your information will be stored anonymously on our server. All information stored can be removed from our server at any time with options in our app that will be covered.

When the required information is filled in and the client has been set up, the user is able to join a session using the chosen *join code*. This join code is unique to one session. On top, two buttons can be found. One of which allows the user to edit or fully delete their previously filled in information. The other simply shows information about the app.

.. image:: images/session.jpg
   :height: 300px
   :align: right

After joining a session, an overview of the session's channel(s) is shown and enables users to select a channel to listen to by simply clicking on it. The color and names of these channels are editable in the control panel. The bottom *pause* button can be clicked if one wants to leave the current channel for a moment. Changing channels can also be fully controlled using the (middle) button on your headphones, just like one would do in a silent disco. On top, two buttons can be found to either refresh the session (that is, reloading all session and channel information) or to leave the session.

Inner workings
------------------
The app allows users to join your silent disco sessions and manage their personal information that is stored. In addition it logs data to the server to improve picking new songs and for (perhaps) research purposes.

Streaming music
^^^^^^^^^^^^^^^^^^^^^
The app's main purpose is playing music streamed by our server. With a silent disco, it is of key importance that all music played on all clients (apps) is played as closely to perfectly synchronous as possible. Minor delays between music played on clients can already have a huge impact. To make sure all clients are *in sync*, the ``NTP`` (= ``Network Time Protocol``) is used.

Logging data
^^^^^^^^^^^^^^^^^^^^^
Another important aspect of the app is the ability to log data back to the server. This data is then used to constantly improve the selection of upcoming songs. It can also be used for research purposes. Right now, both channel switches and movement can be logged to the server. However only channel switches are used as feedback to improve the selection of new music. Thus right now only channel switches are actually sent to the server.

It is however easy to add new data to log. Data logging is done asynchronously in the ``Logger.java`` class. If one wants to add movement (measured via the accelerometer) to log, the ``onSensorChanged`` function can be uncommented and added to the data logging in the ``intervalLogger``. If one wants to log other data (e.g. position) this can also be done in this class.
