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
- Clone repository dari https://gitlab.greatdayhr.com/greatday-devops/nodejs-express-mysql.git
- ```git clone https://gitlab.greatdayhr.com/greatday-devops/nodejs-express-mysql.git```
- ![Screenshot from 2023-12-06 12-26-21](https://github.com/galantixa/GreatDay/assets/92994294/e5188725-6869-48d8-bd0d-87a804df170b)
## Install node js using nvm and install pm2
- Install nodejs via nvm ```curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash```
- ```nvm install 20``` untuk menginstall node versi 10
- pm2 used for manages process nodejs application
- ```npm i -g pm2```
- ```pm2 ecosystem init``` untuk membbuat file konfigurasi pm2
- ![Screenshot from 2023-12-06 12-58-16](https://github.com/galantixa/GreatDay/assets/92994294/f54125e1-07b9-455d-afe1-e7237a48b7e6)
- ![Screenshot from 2023-12-06 13-08-48](https://github.com/galantixa/GreatDay/assets/92994294/01def892-27f2-4843-b3ad-4ad6b4e55578)
- ![Screenshot from 2023-12-06 15-07-32](https://github.com/galantixa/GreatDay/assets/92994294/e205290d-994a-485e-8846-5af667d81b29)
 
## Install mysql server and 
### ganti root password sesuai kebutuhan
- ```sudo apt install mysql-server``` untuk menginstal mysql
- jalankan ```sudo mysql_secure_installation``` untuk mengganti root password
- login mysql dengan user dan password ```sudo mysql -uroot -p``` dan masukan password yang telah kita setup
- ![Screenshot from 2023-12-06 12-33-42](https://github.com/galantixa/GreatDay/assets/92994294/a07fb0e7-e3b4-4980-a69b-5b26dc9d15d9)
- selanjutnya buat database dan baut tabel baru sesuai dengan requirement yang diperlukan
- ```CREATE DATABASE testdb``` ```USE testdb```
- buat tabel baru
 - ```
       CREATE TABLE IF NOT EXISTS `tutorials` (
       id int(11) NOT NULL PRIMARY KEY AUTO_INCREMENT,
       title varchar(255) NOT NULL,
       description varchar(255),
       published BOOLEAN DEFAULT false
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```
- ![Screenshot from 2023-12-06 12-55-46](https://github.com/galantixa/GreatDay/assets/92994294/47d570e8-060a-4022-a4d8-13eb1228f848)
- ![Screenshot from 2023-12-06 12-55-50](https://github.com/galantixa/GreatDay/assets/92994294/749b612f-a95e-4517-8a64-82de2078c427)
- Configure database on nodejs apps ```app/config/db.config.js```
- masukan sesuai dengan user, password, nama database dan host yang telah di setup
- ![Screenshot from 2023-12-06 15-46-01](https://github.com/galantixa/GreatDay/assets/92994294/3f6d8ebb-60ad-4a65-853b-70f8ab52263a)
## Install nginx and configure reverse proxy
- ```sudo apt install nginx``` untuk menginstall nginx
- cek status nginx ```sudo systemctl status nginx```
- ![Screenshot from 2023-12-06 13-06-07](https://github.com/galantixa/GreatDay/assets/92994294/ee89f7df-94cb-4047-b23a-48f22bd498d5)
- konfigurasi reverse proxy untuk expose agar aplikasi bisa diakses public ```sudo nano /etc/nginx/sites-enabled/reverse-proxy.conf```
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
- testing POST request untuk menambahkan data ke database
- ```
    POST http://18.141.176.241/api/tutorials HTTP/1.1
     content-type: application/json
     Access-Control-Allow-Origin: *
     
     {
         "title": "sample",
         "description": "test tutor"
     }
  ```
  - berhasil menambahkan data
  - ```
    HTTP/1.1 200 OK
    Server: nginx/1.18.0 (Ubuntu)
    Date: Wed, 06 Dec 2023 07:51:49 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 70
    Connection: close
    X-Powered-By: Express
    Access-Control-Allow-Origin: http://localhost:8081
    Vary: Origin
    ETag: W/"46-ZdBC+VHi9xjbJF2IOMvXtknMI3E"
    
    {
      "id": 1,
      "title": "sample",
      "description": "test tutor",
      "published": false
    }
  ```
- ![Screenshot from 2023-12-06 14-52-15](https://github.com/galantixa/GreatDay/assets/92994294/27cc4c9b-cc25-40bb-9806-c53dc54effae)
- ![Screenshot from 2023-12-06 16-09-37](https://github.com/galantixa/GreatDay/assets/92994294/6844ca63-5247-4716-82c2-72a26af72847)
## Additional! adding domain and ssl certificate
### Using cerbot
- install certbot ```sudo snap install --classic certbot```
- ![Screenshot from 2023-12-06 16-22-19](https://github.com/galantixa/GreatDay/assets/92994294/af73bef7-3196-4692-9cd3-cd2acdff6ff3)
- ![Screenshot from 2023-12-06 16-15-18](https://github.com/galantixa/GreatDay/assets/92994294/39f5ca0b-4c06-46b0-9b3a-cd2f817bfd4e)
-  ![Screenshot from 2023-12-06 16-14-56](https://github.com/galantixa/GreatDay/assets/92994294/7f6015d4-92c9-4233-83f4-c606c2775d69)
-  ![Screenshot from 2023-12-06 16-14-48](https://github.com/galantixa/GreatDay/assets/92994294/62483c51-8b67-469e-a0ec-5e4f4a76abe3)
- dokumentasi [certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntuother)






