	                 _                                     _                       
	 _ __   ___   __| | ___       ___ _ __   __ _  ___ ___| |__  _ __ _____      __
	| '_ \ / _ \ / _` |/ _ \_____/ __| '_ \ / _` |/ __/ _ \ '_ \| '__/ _ \ \ /\ / /
	| | | | (_) | (_| |  __/_____\__ \ |_) | (_| | (_|  __/ |_) | | |  __/\ V  V / 
	|_| |_|\___/ \__,_|\___|     |___/ .__/ \__,_|\___\___|_.__/|_|  \___| \_/\_/  
	                                 |_|                                           

##Introuction

This module is the [sb-1.4.1.js](https://github.com/Spacebrew/spacebrew.js) you can find at [the main Spacebrew.js repo](https://github.com/Spacebrew/spacebrew.js) but packaged as an NPM Module.  Check out [Getting started with Spacebrew](http://docs.spacebrew.cc/gettingstarted/) for more information about Spacebrew.

##Note

This is a spacebrew CLIENT library. To install a Spacebrew server, check out [Spacebrew on Github](https://github.com/Spacebrew/spacebrew.).

##Setup

The first step is to install the module

	npm install spacebrew-client

Then, in your app, create a Spacebrew object

	var Spacebrew = require('spacebrew-client')

Next, create your Spacebrew client.  

	var server = "sandbox.spacebrew.cc";
	var name = "Clock";
	var description = "Tick tock";
	var sb = new Spacebrew.Client( server, name, description );


##Publishers

Publishers send information to the Spacebrew server that you specify. You can add as many publishers and subscribers as you'd like.  Here is an example publisher:

	sb.addPublish("tick", "string", "The tick of a clock!");  // create the publication feed

	var i = 0;
	setInterval(function(){
	  var newString = "The time is now "+i;
	  sb.send("tick", "string", newString);   // send string to spacebrew
	  i++;
	}, 1000);


## Subscribers

Subscribers will listen for information coming from the Spacebrew server that you specify.  

	sb.addSubscribe("tick", "string");
	sb.onStringMessage = onStringMessage( name, value ){
		if(name=="tick") {
			console.log("Message from server: "+value);
		}
	}

Subscribers will listen for information coming from the Spacebrew server that you specify.  

	sb.addSubscribe("tick", "string");
	sb.onStringMessage = onStringMessage( name, value ){
		if(name=="tick") {
			console.log("Message from server: "+value);
		}
	}


##Connect!

	// connect to spacbrew
	sb.connect();


## Admin Mixin

To use the [Spacebrew Admin Mixin](https://github.com/Spacebrew/spacebrew.js/blob/master/library/sb-admin-0.1.5.js), you can call ``Spacebrew.makeAdmin()``. An example

    var Spacebrew = require( 'spacebrew-client' );
    
    var myAdminClient = new Spacebrew.Client();
    myAdminClient.extend( Spacebrew.makeAdmin() );
    myAdminClient.name( 'MIGHTY SPACEBREW ADMIN' );
    myAdminClient.connect();


before creating a client.
