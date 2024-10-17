
# Web Server

## Install Web Server
update package
```
apt update
```
install nginx
```
apt install nginx
```
## Uji Web Server
uji via CLI/Web browser
```
curl http://172.16.8.250

buka browser
http://172.16.8.250
```

## custom domain
konfigurasi /etc/nginx/sites-available/default
```
server_name academy.id;
```
setelah itu restart service nginx
```
systemctl restart nginx
```

## Uji Web Server
```
curl http://academy.id

buka browser
http://academy.id
```

# Create Certificate Authority, Server Certificate
## Install Openssl
```
apt update && apt install openssl
```
Buat direktori baru di '/etc/ssl'
```
mkdir /etc/ssl/academy.id
```
Generate CA
```
openssl genrsa -des3 -out ca.key 2048
openssl req -x509 -new -nodes -key ca.key -sha256 -days 365 -out ca.pem
```
Create config file
```
cat << EOF >> config.txt
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = academy.id
DNS.2 = *.academy.id
EOF
```
Generate certificate server
```
openssl genrsa -out domain.key 2048
openssl req -new -key domain.key -out domain.csr
openssl x509 -req -in domain.csr -CA ca.pem -CAkey ca.key -CAcreateserial -out domain.crt -days 365 -sha256 -extfile config.txt
```
Konfigurasi virtualhost nginx
```
cat << EOF >> /etc/nginx/sites-available/default
server {
    listen 80;  # Untuk HTTP
    listen 443 ssl;

    ssl_certificate /etc/ssl/academy.id/domain.crt;
    ssl_certificate_key /etc/ssl/academy.id/domain.key;
# Ganti dengan domain atau IP yang ingin Anda gunakan

    location / {
        client_max_body_size 100M;
        proxy_pass http://172.18.0.2;  # Meneruskan ke aplikasi di 127.0.0.1:8080
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
EOF
```
setelah itu restart service nginx
```
systemctl restart nginx
```
