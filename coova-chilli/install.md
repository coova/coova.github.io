---
layout: page
title: CoovaChilli JSON Interface
permalink: /CoovaChilli/JSON/
---

This is a working specification for a new interface JSON interface for
CoovaChilli. Please note that this is different from the existing XML based
interface used for WISPr messages, and extended as a previous attempt for
browser based clients.

Architecture of a Browser Based Smart Client
--------------------------------------------

To communicate with the CoovaChilli Controller, the application uses the methods
exposed by the chilliController javascript object. This object sends commands as
HTTP GET requests to CoovaChilli and receives JSON formatted replies from
CoovaChilli. This chilliController object can issue three main commands to the
Controller:

- **logon**, attempt a CHAP login. The reply will contain the session data and initial accounting data.
- **logoff**, ends the current session.
- **status**, provide the latest accounting data

A Browser Based Smart Client Application downloads the ChilliLibrary.js javascript library and is then be able to use the global chilliController object with three methods:

- **logon**
- **logoff**
- **refresh**

When a client is authorized, the chilliController object will periodically
update accounting data by issuing periodic status commands to refresh the data
(autorefresh).

Only CHAP authentication supported method. The password will never leave the
browser executing the BBSC application.

The security model of both Web browsers and the Flash player will not allow
programmatic HTTP request to URLs residing on a different host/domain/port,
after the containing page/movie is loaded. However, there are workarounds:

*Javascript*: Use DOM API to dynamically create a tag. This will load a JavaScript file from any destination, without security restrictions. This file contains a JSON object passed to a callback function. This callback must already exist in the JS contect of the containing page. See here

*Flash* we can override the default security policy with cross domain policy files as described here
Using these two workarounds, any HTML page (Flash movie), from any domain, can include a single ChilliLibrary.js file (ChilliLibrary.swf) to create a Controller object that will allow communication from the client application to CoovaChilli.

BBSCs could also be implemented as FireFox extensions or IE add-ons.

chilliController interface
--------------------------

JavaScript pseudo code

    <script src="http&#58;//my.host.com/ChilliLibrary.js"></script>
    <script>
    // The included script creates a global chilliController object
  
    // If you use non standard configuration, define your configuration 
    chilliController.host = "10.0.0.1";  // Default is 192.168.182.1
    chilliController.port  = 4003     ; //  Default is 3990
    chilliController.interval = 60    ; // Default is 30 seconds
  
    // then define event handler functions
    chilliController.onError  = handleErrors;
    chilliController.onUpdate = updateUI ;
    
    // when the reply is ready, this handler function is called
    function updateUI( cmd ) {
      alert ( ‘You called the method' + cmd +
        '\n Your current state is =’ + chilliController.clientState ) ;
    }
  
    // If an error occurs, this handler will be called instead
    function handleErrors ( code ) {
      alert ( 'The last contact with the Controller failed. Error code =' + code );
    }
    //  finally, get current state
    chilliController.refresh();
    </script>

Configuration
------------

The chilliController is a global object created by the included script. By
default, it is configured to contact the CoovaChilli gateway at
192.168.182.1:3990 every 30 seconds. If required, you must modify these values
to match your specific configuration before calling a method.

After the chilliController object is configured, you must explicitly call the
refresh method to determine the current state of the client.

Methods
-------

> logon ( username , password )

CHAP login attempt.

> logoff()

Logoff the current session.

> refresh()

Refresh the accounting and session data immediately, i.e. without waiting for
the next scheduled autorefresh.

Properties
----------

--- | ------
host | ip address of the CoovaChilli access controller
port | HTTP port for the JSON requests
interval | in seconds. While the user is authenticated, session/accounting data is refreshed by polling CoovaChilli at this rate,
language | Preferred language for the Reply-Message (Two letter ISO language code, eg. ‘en’).
clientState | State of the terminal. UNKNOWN means that no information has been received from CoovaChilli yet. <ul><li>UNKNOWN (-1)</li><li>NOT_AUTHORIZED (0)</li><li>AUTHORIZED (1)</li><li>AUTH_PENDING (2)</li></ul>
command | last command send to CoovaChilli (may still be pending): logon, logoff, refresh, autorefresh
terminateCause | Same value as the Acct-Terminate-Cause attribute + UNKOWN value when no information from CoovaChilli has been received yet (-1). Not yet implemented. <ul><li>User-Request (1)</li><li>Lost-Carrier (2)</li><li>Idle-Timeout (4)</li><li>Session-Timeout (5)</li><li>NAS-Reboot (11)</li><li>UNKOWN (-1)</li></ul>
sessionId | unique identifier of the session as generated by CoovaChilli (Acct-Session-Id). This is used to make sure the properties found in the session member and the accounting member do belong to the same session.
message | Message to be displayed to the user (Can be the radius Reply-Message or a CoovaChilli generated message)
redir | this member exposes data read on the URL of the initial redirection to uamhomepage. This member will exist only if the uamhomepage is including chilliController.js.... (Alternative: Chilli could memorize it during a session, and always return it in the JSON reply... this would avoid using cookies to store this data to survive the browser being closed )
originalURL | URL originally requested by the client (before the redirection)
redirectionURL | URL to redirecto to next, WISPr-Redirection-URL or otherwise
macAddress | Calling-Station-Id - mac address of the client device
ipAddress | Framed-IP-Address (not yet implemented)
location | this member object contains basic information about the location
name | WISPr-Location-Name - name of the location (chilli.conf locationname or radiuslocationname)
session | this member exposes the radius attributes received in the radius access-accept packet. These attributes are fixed during a session (unless the option to update the properties of a live session is implemented in CoovaChilli)
userName | User-Name (not yet implemented)
startTime | CoovaChilli time session start time. ECMAScript Date object. This one is not a radius attribute, but useful in the BBSC user interface.
terminateTime	| WISPr-Session-Terminate-Time. ECMAScript Date object. (not yet implemented)
sessionTimeout	| Session-Timeout
idleTimeout	| Idle-Timeout
maxInputOctets	| ChilliSpot-Max-Input-Octets (not yet)
maxOutputOctets	| ChilliSpot-Max-Output-Octets (not yet)
maxTotalOctets	| ChilliSpot-Max-Total-Octets (not yet)
bandwidthMaxDown	| WISPr-Bandwidth-Max-Down (not yet)
bandwidthMaxUp	| WISPr-Bandwidth-Max-Up (not yet)
accounting | Volume/Time accounting attributes. These attributes will change during a session.
sessionTime	| Acct-Session-Time - session duration
idleTime	| Idle time calculated by CoovaChilli (traffic to/from CoovaChilli is ignored). This one is not a radius attribute, but the Controller object will use it to schedule the next refresh just after a likely IdleTimeout disconnection. It's also exposed in the API, to be comprehensive.
inputOctets	| Acct-Input-Octets
outputOctets |	Acct-Output-Octets
inputGigawords	| Acct-Input-Gigawords
outputGigawords	| Acct-Output-Gigawords

Event handlers
-------------

**onUpdate**

Handler function called when the chilliController object has been
updated. Updates are triggered when new data has been received from the
controller. This is the case:

- after a method is explicitly called (logon,logoff,refresh)
- automatically every interval seconds, when the client is authorized (autorefresh)

The handler function receives the name of the command that triggered the update
as an argument (logon,logoff,refresh,autorefresh).

**onError**

Handler function called when a correct JSON response cannot be obtained from the controller. (e.g. wireless link down, wrong JSON syntax,....). The handler function receives an error code as an argument.

Interface to CoovaChilli
========================

Commands are send to CoovaChilli with HTTP requests. The lang GET parameter is
used on all URLs to pass the preferred language (only used in logon for the time
being).

The version field is used to track different versions of the CoovaChilli JSON protocol.

If a callback parameter (callback=function) is present, then CoovaChilli will
wrap the JSON output text in parentheses and prepend it with the callback
function. The output will look like a function call with a JSON object passed as
parameter. This will allow cross domain access to the JSON feed from JavaScript.

Logon
-----

When the logon() method of the Controller object is called, the Controller object:

- generates a random CHAP-challenge (hex string)
- requests http://192.168.182.1:3990/json/logon?username=XXXX&chapchallenge=YYYY&chappassword=0123456789abcdef&lang=EN

CoovaChilli replies with a JSON formated object like this

    {
      "version" : "1.0",
      "clientState" : 1 ,
      "sessionId" : "4662e92b0000000e" ,
      "message" : "You’re now connected" ,
      "location" : {
         "name":  "Coova labs"
      },
 
      "redir" : {
        "macAddress" : "00-30-1B-B5-03-6B",
        "originalURL" : "http://my.yahoo.com/",
        "redirectionURL" : "http://www.coova.org/welcome.php",
        "ipAddress" : "192.168.182.47"
      },
 
      "session" : {
        "startTime" : 137550720,
        "terminateTime" : 13756072,
        "sessionTimeout" : 3600,
        "idleTimeout" : 240,
        "maxInputOctets" : 100000000,
        "maxOutputOctets" : 100000000,
        "maxTotalOctets" : 100000000,
        "bandwidthMaxDown" : 1000000,
        "bandwidthMaxUp" : 1000000
      },
  
      "accounting": {
         "sessionTime" : 2,
         "idleTime" : 0,
         "inputOctets" : 0,
         "outputOctets" : 0,
         "inputGigawords" : 0,
         "outputGigawords" : 0
      }
    }

If the authorization, does not succeed. The JSON reply will look like this

    {
      "version": "1.0",
      "clientState": 0,
      "message": "This username does not exist",
      "location" : { "name":"My HotSpot" }
     }

Logoff
-----

Request to http://192.168.182.1:3990/json/logoff?lang=en&callback=myfunc

The JSON reply will look like this:

     myfunc ( { "version": "1.0", "clientState": 0 } )
     
Status refresh
--------------

Request to http://192.168.182.1:3990/json/status?lang=en

The JSON reply will look like this:
 
    {
     "version" : "1.0",
     "clientState" : 1 ,
     "sessionId" : "4662e92b0000000e" ,
     "accounting": {
         "sessionTime" : 1230,
         "idleTime" : 240,
         "inputOctets" : 2912981 ,
         "outputOctets" : 51498511,
         "inputGigawords" : 0,
         "outputGigawords" : 0
      }
    }
    
It's not necessary to repeat the fixed session properties here. The sessionId is used to associate the newly received accounting values with the session values received with the initial logon command.

Problem: What if a someone uses the HTML form to connect and then uses a BBSC for status display?

If the client is not authorized:

    {
     "version" : "1.0",
     "clientState" : 0
    }


