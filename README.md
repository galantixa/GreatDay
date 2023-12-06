#  GreatDay Tech Test
### Requirement
- node
- npm
- pm2
- nginx
- mysql server

## SSH to the server using private keys
- ![Screenshot from 2023-12-06 12-21-28](https://github.com/galantixa/GreatDay/assets/92994294/86c365f2-a2b1-4843-925d-0ef293fb6ba3)
## Clone repository
- ![Screenshot from 2023-12-06 12-26-21](https://github.com/galantixa/GreatDay/assets/92994294/e5188725-6869-48d8-bd0d-87a804df170b)
## Install node js using nvm and install pm2
- ![Screenshot from 2023-12-06 12-58-16](https://github.com/galantixa/GreatDay/assets/92994294/f54125e1-07b9-455d-afe1-e7237a48b7e6)
- ![Screenshot from 2023-12-06 13-08-48](https://github.com/galantixa/GreatDay/assets/92994294/01def892-27f2-4843-b3ad-4ad6b4e55578)
- ![Screenshot from 2023-12-06 15-07-32](https://github.com/galantixa/GreatDay/assets/92994294/e205290d-994a-485e-8846-5af667d81b29)
 
## Install mysql server and ```sudo mysql_secure_installation```
### ganti root password sesuai kebutuhan
- ![Screenshot from 2023-12-06 12-33-42](https://github.com/galantixa/GreatDay/assets/92994294/a07fb0e7-e3b4-4980-a69b-5b26dc9d15d9)
- ![Screenshot from 2023-12-06 12-55-46](https://github.com/galantixa/GreatDay/assets/92994294/47d570e8-060a-4022-a4d8-13eb1228f848)
- ![Screenshot from 2023-12-06 12-55-50](https://github.com/galantixa/GreatDay/assets/92994294/749b612f-a95e-4517-8a64-82de2078c427)
### Configure database on nodejs apps ```app/config/db.config.js```
- ![Screenshot from 2023-12-06 15-46-01](https://github.com/galantixa/GreatDay/assets/92994294/3f6d8ebb-60ad-4a65-853b-70f8ab52263a)
## Install nginx and configure reverse proxy
- ![Screenshot from 2023-12-06 13-06-07](https://github.com/galantixa/GreatDay/assets/92994294/ee89f7df-94cb-4047-b23a-48f22bd498d5)
- reverse proxy ```reverse-proxy.conf``` ```/etc/nginx/sites enabled```
- ```
    server { 
      listen 80;
      server_name 18.141.176.241;
  
      location / { 
               proxy_pass http://172.31.16.170:8080;
      }
  }
  ```
- Validasi dan reload nginx ```sudo nginx -t``` ```sudo systemctl reload nginx```
## masuk folder ```nodejs-express-mysql``` dan jalankan ```pm2 start```
- ![Screenshot from 2023-12-06 15-15-06](https://github.com/galantixa/GreatDay/assets/92994294/e95d8a3a-2ca0-44cd-b82e-86f4482fa3fe)
## Result
- ![Screenshot from 2023-12-06 14-52-15](https://github.com/galantixa/GreatDay/assets/92994294/27cc4c9b-cc25-40bb-9806-c53dc54effae)
- ![Screenshot from 2023-12-06 16-09-37](https://github.com/galantixa/GreatDay/assets/92994294/6844ca63-5247-4716-82c2-72a26af72847)
## Additional! adding domain and ssl certificate
### Using cerbot
- ![Screenshot from 2023-12-06 16-22-19](https://github.com/galantixa/GreatDay/assets/92994294/af73bef7-3196-4692-9cd3-cd2acdff6ff3)
- ![Screenshot from 2023-12-06 16-15-18](https://github.com/galantixa/GreatDay/assets/92994294/39f5ca0b-4c06-46b0-9b3a-cd2f817bfd4e)
-  ![Screenshot from 2023-12-06 16-14-56](https://github.com/galantixa/GreatDay/assets/92994294/7f6015d4-92c9-4233-83f4-c606c2775d69)
-  ![Screenshot from 2023-12-06 16-14-48](https://github.com/galantixa/GreatDay/assets/92994294/62483c51-8b67-469e-a0ec-5e4f4a76abe3)







