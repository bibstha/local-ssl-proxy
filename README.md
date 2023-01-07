# local-ssl-proxy
A super simple docker and Caddy config to route local domain names to services running on host or other docker containers

## Steps

**1. Create an entry manually in /etc/hosts**
```
cat /etc/hosts
127.0.0.1 localhost
::1       localhost
127.0.0.1 myapp1.localhost myapp2.localhost
```

**2. Clone this repository**
```
git clone https://github.com/bibstha/local-ssl-proxy.git
cd local-ssl-proxy
```

**3. Copy Caddyfile.example to Caddyfile**
```
cp Caddyfile.example Caddyfile
```
Or simply create a new file and add the following.


**4. Make changes to set the right apps**
```
cat Caddyfile
myapp1.localhost
reverse_proxy http://host.docker.internal:PORT_OF_myapp1

myapp2.localhost
reverse_proxy http://host.docker.internal:PORT_OF_myapp2
```

**5. Start caddy**
```
docker compose up -d
```

**6. Load your app in the browser**

https://myapp1.localhost

**Note**: You will have to accept the certificate as trusted as this is self signed by caddy. You will only have to do this once.
