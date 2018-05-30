<h1>Comparison of Telegram and Viber bots</h1>

---

@[intro]
<h2>Why bot?</h2>
@ul
 * Mobile app is too heavy solution.
 * It is not getting lost when using it one a month.
 * It knows your phone number.
@ulend
---

<h1>Configuration</h1>

+++

@[Bot Father vs Web-Mobile-Nothing]

<h2>Create it!</h2>

@div[left-50]
<h1>tg</h1>
<h2>Bot Father</h2>
@divend

@div[right-50]
<h1>viber</h1>
<h2>Web-Mobile-Nothing</h2>
@divend

+++

@[https]

<h2>https</h2>

@div[left-50]
<h1>tg</h1>
<h2>Self-signed certificate</h2>

@divend

@div[right-50]
<h1>viber</h1>
<h2>CA</h2>
@divend

+++

@[how-to-communicate]

<h2>Communication</h2>

@div[left-50]
<h1>tg</h1>

@ul
 - webhook -> response
 - webhook -> callback
 - long poll -> callback
@ulend

@divend

@div[right-50]
<h1>viber</h1>

@ul
 * webhook -> callback 
 * only 
 * almost only...
@ulend

@divend

+++

@[client]

<h2>How to use it?</h2>

@div[left-50]
<h1>tg</h1>
@ul
 - mobile
 - desktop
 - web
@ulend
@divend

@div[right-50]
<h1>viber</h1>
@ul
 * mobile
 * only  
@ulend
@divend

---

<h1>API</h1>
<h5>Data structure</h5>

+++

@[sender-receiver]

<h2>Documentation</h2>

@div[left-50]
<h1>tg</h1>
@ul
 - consistent
 - browsable (with anchor links to data types)
 - big plain message
@ulend
@divend

@div[right-50]
<h1>viber</h1>
@ul
 * ad hoc (?)
 * non-browsable
 * different types of message (as declared)
@ulend
@divend

+++

<h4>Message example</h4>
```
{
   "receiver":"01234567890A=",
   "min_api_version":1,
   "sender":{
      "name":"John McClane",
      "avatar":"http://avatar.example.com"
   },
   "tracking_data":"tracking data",
   "type":"text",
   "text":"Hello world!"
}
```
@[2]
@[3]
@[4-7]
@[8]
@[9]
@[10]

+++

Text

```
{
   "receiver":"01234567890A=",
   "sender":{
      "name":"John McClane"
   },
   "type":"text",
   "text":"Hello world!"
}
```
@[6-7]

+++

File

```
{  
   "receiver":"01234567890A=",
   "sender":{  
      "name":"John McClane",
   },
   "type":"file",
   "media":"http://www.images.com/file.doc",
   "size":10000,
   "file_name":"name_of_file.doc"
}
```
@[6-9]

+++

Contact

```
{
   "receiver":"01234567890A=",
   "sender":{
      "name":"John McClane",
   },
   "type":"contact",
   "contact":{
      "name":"Itamar",
      "phone_number":"+972511123123"
   }
}
```
@[6-10]

+++

Location

```
{
   "receiver":"01234567890A=",
   "sender":{
      "name":"John McClane",
   },
   "type":"location",
   "location":{
      "lat":"37.7898",
      "lon":"-122.3942"
   }
}
```
@[6-11]

+++

Also `Picture`, `Video`, `URL`, `Sticker` and `rich-media`

+++

<h5> How do they propose to handle it with python? </h5>

```
# this library supplies a simple way to receive a request object
viber_request = viber.parse_request(request.get_data())

if isinstance(viber_request, ViberMessageRequest):
    message = viber_request.message
    # lets echo back
    viber.send_messages(viber_request.sender.id, [
        message
    ])
elif isinstance(viber_request, ViberSubscribedRequest):
    viber.send_messages(viber_request.get_user.id, [
        TextMessage(text="thanks for subscribing!")
    ])
elif isinstance(viber_request, ViberFailedRequest):
    logger.warn("client failed receiving message. failure: {0}".format(viber_request))
```
@[1-2]
@[10]

+++

<h4>Viber, why?</h4>

@div[left-50]
<h1>tg</h1>
@ul
 - Bot Father message
 - Reusable connection in python client
@ulend
@divend

@div[right-50]
<h1>viber</h1>
@ul
 * Response message
 * <b>user</b> keyword instead of <b>sender</b>
 * requests.post
@ulend
@divend

+++

<h5> Quote from official docs </h5>

@ul
 * User opens 1-on-1 conversation with account.
 * Viber server send `conversation_started` even to PA’s webhook.
 * The account receives the `conversation_started` and **responds** with an HTTP response which includes the welcome message as the **response body**.
 * ...
 * An example welcome message would look like this:
@ulend 

```
@app.route('/', methods=['POST'])
def incoming():
	   viber_request = viber.parse_request(request.get_data())

	   if isinstance(viber_request, ViberConversationStartedRequest) :
		      viber.send_messages(viber_request.get_user().get_id(), [
			         TextMessage(text="Welcome!")
		      ])

	   return Response(status=200)
```
@[10]

+++

<h2>Keyboards</h2>

@div[left-50]
<h1>tg</h1>
@ul
 - Not customizable 
 - Text button vs inline button
@ulend
@divend

@div[right-50]
<h1>viber</h1>
@ul
 * Infinite customization
 * Text-AND-callback buttons
 * Hide text input
@ulend
@divend

---






