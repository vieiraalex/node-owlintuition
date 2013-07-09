node-owlintuition
=================

node.js library for the [OWL Intuition range](http://www.theowl.com) of energy monitoring and control systems. It has been tested against v2.0 and v2.1 of the Network OWL firmware.

Install
-------

npm install owlintuition

Usage
-----

Create an instance of the owl class and connect to the multicast broadcast from the Network OWL,

    var OWL = require('owl');
	monitor.connect();

you can subscribe to four different event messages. The first message is for electricity updates,
	
	monitor.on('electricity', function( event ) {

	});
	
where you will receive an event object of the form,
	
	{"id":"443719001958",
	 "signal":
	    {"rssi":"-66",
	     "lqi":"127"},
	 "battery":"100%",
	 "channels":
	    {"0":[
	        {"current":"241.00", "units":"w"},
	        {"day":"823.49", "units":"wh"}],
	     "1":[
	        {"current":"0.00", "units":"w"},
	        {"day":"0.00", "units":"wh"}],
	     "2":[
	        {"current":"0.00", "units":"w"},
	        {"day":"0.00", "units":"wh"}]}}		

as an argument to your callback function. The second message is for heating updates, and will only occur if a Intuition-c Room Monitor has been installed,	

	monitor.on('heating', function( event ) {
		
	});

where you will receive an event object of the form, 
	
      {"id":443719001958,
       "signal":
          {"rssi":-66,
           "lqi":49},
       "battery":"2970mV",
       "temperature":
          {"until":1373409000,
           "zone":0,
           "current":21.25,
           "required":20}}
	
passed back as an argument to your callback function. The third and last message type is for periodic local weather updates,

	monitor.on('weather', function( event ) {
		
	});
	
where you will receive an event object of the form,

      {"id":443719001958,
       "code":113,
       "temperature":"26.01",
       "text":"Clear/Sunny"}
	
passed back to your callback function. Finally the fourth message is for solar updates,

    monitor.on('solar', function(event) {
	
    });

where you will receive an event object of the form

      {"id":"443719001958",
       "current":[
          {"generating":1000,"units":"w"},
          {"exporting":730, "units":"w"}],
       "day":[
          {"generated":23000, "units":"wh"},
          {"exported":17000, "units":"wh"}]}

There is also an error message if the module encounters a 'new' unknown message over multicast,

	monitor.on('error', function( message ) {
	
	});	
	
where a string describing the error will be returned.

# LICENSE

This software is distributed under the [MIT](http://en.wikipedia.org/wiki/MIT_License) license.

Copyright (C) 2013 Alasdair Allan <alasdair@babilim.co.uk>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
