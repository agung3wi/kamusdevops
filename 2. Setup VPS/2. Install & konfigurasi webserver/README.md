# Install & konfigurasi webserver (Nginx)

> Nginx adalah salah satu server web terpopuler di dunia dan berperan sebagai hos dari sebagian situs terbesar dan situs yang memiliki lalu lintas tertinggi di jagad internet. [Referensi](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04-id)

#### Instalasi nginx
```
sudo apt update
sudo apt install nginx
```

#### Memeriksa Server web
Dengan sistem init *systemd* untuk memastikan layanan sedang berjalan dengan command 
```
systemctl status nginx
```

Untuk menghentikan server web
```
sudo systemctl stop nginx
```

Untuk menjalankan server web
```
sudo systemctl start nginx
```

Untuk menghentikan lalu menjalankan layanan lagi
```
sudo systemctl restart nginx
```

#### Konfigurasi Server
* **/etc/nginx** => Direktori konfigurasi nginx. Semua berkas konfigurasi nginx ada disini.
* **/etc/nginx/nginx.conf** => Berkas konfigurasi nginx utama.
* **/etc/nginx/sites-enabled/** => Direktori tempat blok server yang diaktifkan per situs disimpan.
* **/etc/nginx/sites-available/** => Direktori tempat blok server per situs dapat disimpan.
* **/etc/nginx/snippets** => Direktori berisi fragmen konfigurasi yang dapat disertakan di tempat lain dalam konfigurasi nginx.


#### Menyiapkan Host Server
1. Masuk ke direktori **/etc/nginx/sites-enabled/**.
2. Buat file sesuai dengan nama host atau subdomain yang dibuat
`nano host_kamu.com`
3. Masukkan konfigurasi berikut kedalam file yang dibuat tadi
```
server {
        listen 80;
        listen [::]:80;

        root /var/www/host_kamu.com/public;
        index index.html index.htm index.nginx-debian.html;

        server_name host_kamu.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

4. Restart kembali nginx 
```
sudo systemctl restart nginx
```

5. Buat direktori untuk domain/subdomain yang dibuat tadi (sesuai dengan yang ada di konfigurasi tadi).
```
mkdir /var/www/host_kamu.com/public
```

6. Buat dan isi file index.html
```
nano index.html
```

# Konfigurasi DNS Server

> Sebagai contoh menggunakan DNS yang dibeli melalu domainesia
1. Siapkan domain terlebih dahulu. 
2. Kemudian manage DNS record. Masuk ke **Addons > DNS Host Record Management >  Manage**
3. Tambahkan subdomain pada `Add new DNS Record`. Pada bagian address masukkan IP Public dari server kalian.