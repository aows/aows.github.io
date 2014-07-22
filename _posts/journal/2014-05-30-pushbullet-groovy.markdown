---
layout: post
title:  "Pushbullet with Groovy"
date:   2014-05-30 16:58:48
categories: journal
---

I'd forgotten, but about a month ago I implemented this simple Groovy script to send a notification using Pushbullet API: [https://gist.github.com/aows/91aff80e03c95104d06c﻿](https://gist.github.com/aows/91aff80e03c95104d06c﻿)

**Update** Oh well, just realized they've released [a new API](http://blog.pushbullet.com/2014/05/15/a-new-and-much-more-powerful-api/) two weeks ago. The script should still work fine though.﻿

{% highlight java %}
import static groovyx.net.http.Method.GET
import static groovyx.net.http.Method.POST
import static groovyx.net.http.ContentType.JSON
import groovy.json.JsonSlurper
@Grab(group='org.codehaus.groovy.modules.http-builder', module='http-builder', version='0.7' )
class GroovyBullet {
	def apikey
	def http = new groovyx.net.http.HTTPBuilder('https://api.pushbullet.com/api/')
 
	GroovyBullet( apikey ) {
		this.apikey = apikey
	}
 
	Collection getDevices() {
		http.request( GET, JSON ) {
			uri.path = 'devices'
			headers.'Authorization' = "Basic ${apikey.bytes.encodeBase64().toString()}"
 
			response.success = { resp, json ->
				return json.devices
			}
		}
	}
 
	void sendNote( iden, title, text ) {
		send( iden, [type: 'note', title: title, body: text] )
	}
 
	void sendLink( iden, title, url ) {
		send( iden, [type: 'link', url: url, title: title] )
	}
 
	private void send ( iden, requestBody ) {
		requestBody.putAll( [device_iden: iden] )
		http.request( POST, JSON ) {
			uri.path = 'pushes'
			headers.'Authorization' = "Basic ${apikey.bytes.encodeBase64().toString()}"
			body = requestBody
		}		
	}	
}
 
def apikey = "apikey"
def groovyBullet = new GroovyBullet( apikey )
def iden = groovyBullet.getDevices()[0].iden
groovyBullet.sendNote(iden, 'hi from PDX', '')
groovyBullet.sendLink(iden, 'hi from PDX', 'http://www.google.com')
{% endhighlight %}