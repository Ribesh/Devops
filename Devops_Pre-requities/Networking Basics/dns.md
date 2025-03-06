# DNS

Name Resolution (adding entry in hosts file)
```bash
cat /etc/hosts
```

If any IP address of the machine changes we have to update it manually in every host file

To overcome this, we point to a DNS server and only change once in ```/etc/hosts``` file

On Local Machine
```bash
cat /etc/resolv.conf
```

By default, any machine first looks at the ```/etc/hosts``` file before cheching in with dns ```/etc/resolv.conf```

To change this order (First look into dns then only hosts file)

```bash
cat /etc/nsswitch.conf

...
hosts:  files dns
...

```

Change it to

```bash
...
hosts:  dns files
...

```

Nslookup only queries the DNS server (Doesn't query the local host)
```bash
nslookup www.google.com
```