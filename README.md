# DVWA-writeups


Damn Vulnerable Web Application writeups


In a linux environemnt 

```Bash
sudo apt update
sudo apt install -y docker.io 
sudo systemctl enable docker --now
docker 
```

and then run 

```bash
sudo docker run --rm -it -p 80:80 vulnerables/web-dvwa 
```

To run the dvwa application.


Go to http://127.0.0.1 and login as 
admin:password

then **Create/Reset Database**

After it has reloaded, login again as admin:password

For other ways of installing it , checkout the official github repository

https://github.com/digininja/DVWA

