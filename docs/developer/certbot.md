# Hướng dẫn cài đặt CertBot

## Giới thiệu
> Tips hướng dẫn cài đặt SSL miễn phí cho nginx trên Centos sử dụng CertBot

- Link tham khảo: [Link](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-centos-7)

## Các bước
### Step 1: Insstall the CertBot let's encrypt client
```sh
sudo yum install epel-release
sudo yum install certbot-nginx
```

### Step 2 — Setting up Nginx (nếu đã có nginx sẵn có thể bỏ qua)
```sh
sudo yum install nginx
sudo systemctl start nginx
sudo vi /etc/nginx/nginx.conf
```

- Find the existing server_name line:
`/etc/nginx/sites-available/default`
> server_name _;

- Replace the _ underscore with your domain name:
`/etc/nginx/nginx.conf`
> server_name example.com www.example.com;

```sh
sudo nginx -t
sudo systemctl reload nginx
```


### Step 3 — Updating the Firewall
```sh
sudo firewall-cmd --add-service=http
sudo firewall-cmd --add-service=https
sudo firewall-cmd --runtime-to-permanent

sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
```


### Step 4 — Obtaining a Certificate
```sh
sudo certbot --nginx -d www.gw.medic247.net.com -d www.gw.medic247.net.com
```
### Step 5 — Updating Diffie-Hellman Parameters
```sh
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

### Step 6 — Setting Up Auto Renewal
```sh
sudo crontab -e
15 3 * * * /usr/bin/certbot renew --quiet
```
