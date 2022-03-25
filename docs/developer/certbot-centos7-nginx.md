# Hướng dẫn cài đặt CertBot - Lets Encrypt cho nginx trên CentOS 7


> Let’s Encrypt là Tổ chức phát hành chứng chỉ (CA) cung cấp và cài đặt chứng chỉ TLS / SSL miễn phí cho phép HTTPS được mã hóa trên máy chủ web

## Thao tác cài đặt Let’s Encrypt cho Nginx trên Centos 7

1. Cài đặt EPEL repository

`sudo yum install epel-release -y`

2. Cài đặt certbot-nginx

`sudo yum install certbot-nginx -y`

3. Cài đặt nginx, các bạn có thể bỏ qua bước cài đặt nginx nếu đã có nginx rồi nhé

`sudo yum install nginx`

4. Khởi động nginx

`sudo systemctl start nginx`

> Certbot có thể tự động định cấu hình SSL cho Ngin
> Nếu các bạn có Firewall thì cần đảm bảo rằng các bạn đã mở port http và https nhé

- Mở port trên FirewallD
```sh
sudo firewall-cmd --add-service=http  
sudo firewall-cmd --add-service=https  
sudo firewall-cmd --runtime-to-permanent
```

- Mở port trên iptables
```sh
sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT  
sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
```

5. Lấy chứng chỉ
```sh
sudo certbot --nginx -d example.com -d www.example.com
```

> Chạy certbot với --nginx, sử dụng -d để chỉ định các tên miền mà bạn muốn lấy chứng chỉ.

> Nếu cài đặt thành công, certbot sẽ hỏi bạn muốn định cấu hình cài đặt HTTPS của mình như thế nào:

- Màn hình output
```sh
Please choose whether HTTPS access is required or optional.  
\-------------------------------------------------------------------------------  
1: Easy - Allow both HTTP and HTTPS access to these sites  
2: Secure - Make all requests redirect to secure HTTPS access  
\-------------------------------------------------------------------------------  
Select the appropriate number \[1-2\] then \[enter\] (press 'c' to cancel):
```

> Chọn lựa chọn của bạn rồi nhấn ENTER. Cấu hình sẽ được cập nhật và Nginx sẽ tải lại để chọn cài đặt mới. certbot sẽ kết thúc bằng một thông báo cho bạn biết quá trình đã thành công và nơi lưu trữ chứng chỉ của bạn:

- Màn hình output
```sh
IMPORTANT NOTES:  
\- Congratulations! Your certificate and chain have been saved at  
   /etc/letsencrypt/live/example.com/fullchain.pem. Your cert will  
   expire on 2017-10-23. To obtain a new or tweaked version of this  
   certificate in the future, simply run certbot again with the  
   "certonly" option. To non-interactively renew \*all\* of your  
   certificates, run "certbot renew"  
\- Your account credentials have been saved in your Certbot  
   configuration directory at /etc/letsencrypt. You should make a  
   secure backup of this folder now. This configuration directory will  
   also contain certificates and private keys obtained by Certbot so  
   making regular backups of this folder is ideal.  
\- If you like Certbot, please consider supporting our work by:  
   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate  
   Donating to EFF:                    https://eff.org/donate-le
```
6. Kiểm tra lại cấu hình
```sh
sudo nginx -t
```

7. Nếu không có lỗi gì thì reload lại nginx
```sh
sudo systemctl reload nginx
```

# Chúc các bạn thành công.