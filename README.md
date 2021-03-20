# Diagram (3 Tier)

![3 Tier](/images/app.png)



# 1. Install Nginx & Configure reverse proxy

[Ansible playbook provided](./nginx.yaml)


# 2. Install PostgreSQL & Create User/DB

[Ansible Playbook provided](./psql.yaml)


# 3. Python App


## [Python App](./app/app.py)

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello World!'

#Listen any can also be changed to specific interface.
app.run(host='10.10.10.11', port=8080)
```

## [requirements](./app/requirements.txt)
`pip3 install -r requirement.txt`

## Execute python app.
`cd hello_world_app; python3 app.py`

Assumption & interpretations: This is not a production grade app or way of running python code in actual environment, we could probably run supervisor or any other tool to make it run on background.

### Assumption & interpretations

Flask based app may not be considered for production use, instead Django may be better suited.
However for the demo purpose we will consider flask a usable python framework and run our app.

We should also consider that webapp running on 8080 port means, we need some proxy/reverse-proxy or loadbalancer in front of these app.
We can consider Nginx (Question 1) as loadbalancer/reverse-proxy.

Nginx should be considered as reverse-proxy which listens on HTTP/HTTPS ports (80/443) and proxied to backend python app port 8080 (as seen in this demo flask app example.)

# 4.  Persistent after reboot.

Nginx & psql (`enabled: true`)

Python App (This would be something like i mentioned above running with supervisor or even docker.)
