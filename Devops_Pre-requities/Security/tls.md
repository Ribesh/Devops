

## Passwordless Authentication
```bash 
sudo ssh-keygen 

Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
/root/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa
```

Copy the public key to the destination server 
```bash
ssh-copy-id -i mykey.pub thor@app01 # this command copies the public_key to ~/.ssh/authorized_keys for passwordless authentication
```

SSH to remote machine using private key (specify the location)
```bash
ssh -i mykey thor@app01
```



## Install Openssl
```bash
sudo yum install -y openssl
```


### Create a CSR (Certificate Signing Request)
```bash
sudo openssl req -new -newkey rsa:2048 -nodes -keyout app01.key -out app01.csr
```

### Verify the entries used to create CSR
```bash
openssl req  -noout -text -in app01.csr
```

In apache web server where SSL is already enabled update the SSL certificates

```bash
vi /etc/httpd/conf.d/ssl.conf
```

```bash
SSLCertificateFile /etc/httpd/certs/app01.crt
SSLCertificateKeyFile /etc/httpd/certs/app01.key
```


To test if server is using correct certificate (check if it returns your certificate)
```bash
echo | openssl s_client -showcerts -servername app01.com -connect app01:443 2>/dev/null | openssl x509 -inform pem
```