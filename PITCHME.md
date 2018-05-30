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
 * ad hoc
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
@[1]
@[2]
@[3-6]
@[7]
@[8]
@[9]

+++

<h4>Viber message types</h4>

@div[left-50]

Text
```json
{
   "receiver":"01234567890A=",
   "sender":{
      "name":"John McClane"
   },
   "type":"text",
   "text":"Hello world!"
}
```
@[5-6]

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
@[5-8]
@divend

@div[right-50]
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
@[5-9]

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
@[5-10]
@divend

+++


