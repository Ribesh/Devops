# Apache Web Server

Install apache web server
```bash
yum install httpd
```

Check service
```bash
systemctl status httpd
systemctl start httpd
```

Allow from firewall
```bash
firewall-cmd --permanent --add-serveice=http
```

View logs
```bash
cat /var/log/httpd/access_log

cat /var/log/httpd/error_log
```

Config File
```bash
vi /etc/httpd/conf/httpd.conf

....
Listen 80

DocumentRoot "/var/www/html"

ServerName www.ribesh.com
....
```

Access the webserver from ``` http://localhost```