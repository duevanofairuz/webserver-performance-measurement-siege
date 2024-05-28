# webserver-performance-measurement-siege - ETS Pemrograman Jaringan Kelas C

## Cara menjalankan:
1. Clone repository `https://github.com/rm77/progjar.git`
2. Jalankan docker melalui wsl
3. Jalankan command:
```
cd progjar/environment
docker compose up -d
```
4. Akses mesin di browser menggunakan format:
```
localhost:[port-mesin1]
localhost:[port-mesin2]
dst..
```
cara yang lebih lengkap ada di: <a href="https://github.com/rm77/progjar/tree/master/environment">sini</a>

## Setup siege
```
sudo apt-get update && sudo apt-get upgrade --show-upgraded
sudo apt-get install build-essential
sudo apt-get install libssl-dev
wget http://download.joedog.org/siege/siege-latest.tar.gz
tar -zxvf siege-latest.tar.gz
cd siege-*/

which openssl 

./configure --prefix=/usr/local --with-ssl=[replace with path above]
sudo make clean
make
sudo make install
```
referensi: <a href="https://stackoverflow.com/questions/42367606/siege-https-error-https-requires-libssl">disini</a>

## Pengetesan
Jalankan program server di atas, lalu buka terminal lain di mesin yang sama (atau di mesin yang berbeda)

Untuk menguji 1000 request dengan concurrent 10, 50, 100, 150, 200 bisa menggunakan command berikut: </br>
`siege -c [jumlah-concurrent] -r [repetisi] [link-server:port]`

link server berupa ip address dari mesin yang dijalankan, contoh: </br>
* link server multithread no secure di mesin 1 </br>
`http://172.16.16.101:8889/`
* link server multithread secure di mesin 1 </br>
`https://172.16.16.101:8443/`

contoh menggunakan siege untuk concurrency 200 di multithread nosecure mesin 1: <br>
`siege -c 200 -r 5 http://172.16.16.101:8889/`