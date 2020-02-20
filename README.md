# SoalShiftSISOP20_modul1_C6

## Soal 2

Pada suatu siang, laptop Randolf dan Afairuzr dibajak oleh seseorang dan kehilangan
data-data penting. Untuk mencegah kejadian yang sama terulang kembali mereka
meminta bantuan kepada Whits karena dia adalah seorang yang punya banyak ide.
Whits memikirkan sebuah ide namun dia meminta bantuan kalian kembali agar ide
tersebut cepat diselesaikan. Idenya adalah kalian (a) membuat sebuah script bash yang
dapat menghasilkan password secara acak sebanyak 28 karakter yang terdapat huruf
besar, huruf kecil, dan angka. (b) Password acak tersebut disimpan pada file berekstensi
.txt dengan nama berdasarkan argumen yang diinputkan dan HANYA berupa alphabet.
(c) Kemudian supaya file .txt tersebut tidak mudah diketahui maka nama filenya akan di
enkripsi dengan menggunakan konversi huruf (string manipulation) yang disesuaikan
dengan jam(0-23) dibuatnya file tersebut dengan program terpisah dengan (misal:
password.txt dibuat pada jam 01.28 maka namanya berubah menjadi qbttxpse.txt
dengan perintah ‘bash soal2_enkripsi.sh password.txt’. Karena p adalah huruf ke 16 dan
file dibuat pada jam 1 maka 16+1=17 dan huruf ke 17 adalah q dan begitu pula
seterusnya. Apabila melebihi z, akan kembali ke a, contoh: huruf w dengan jam 5.28,
maka akan menjadi huruf b.) dan (d) jangan lupa untuk membuat dekripsinya supaya
nama file bisa kembali.
HINT: enkripsi yang digunakan adalah caesar cipher.
*Gunakan Bash Script

## Penyelesaian

```
#!bin/bash

answer=$@
p=${#answer}
a=$(expr "$answer" : "[A-Za-z]*$")

if [ $p -eq $a ]
then
	cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 28 | head -n 1 > /home/afif/sisop/mod/$@.txt
else
	echo "argument hanya berupa alphabet"
fi

now=$(date +%H)

echo $answer| tr $(printf %${now}s | tr ' ' '.')\A-Z A-ZA-Z | tr $(printf %${now}s | tr ' ' '.')\a-z a-za-z > /home/afif/sisop/mod/afif.txt

num=$(cat /home/afif/sisop/mod/afif.txt)

mv  /home/afif/sisop/mod/$answer.txt /home/afif/sisop/mod/$num.txt

rm /home/afif/sisop/mod/afif.txt
```

```
#!bin/bash

answer=$@
p=${#answer}
a=$(expr "$answer" : "[A-Za-z]*$")
```
Fungsi berikut ini untuk mengambil input argumen dan menghitung panjang string serta menghitung panjang string yang mengandung alphabet atau huruf

```
if [ $p -eq $a ]
then
	cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 28 | head -n 1 > /home/afif/sisop/mod/$@.txt
else
	echo "argument hanya berupa alphabet"
fi
```

Untuk mengecek apakah semua isi dari argumen itu adalah alphabet. Jika iya, maka program akan generate password yang panjangnya 28 dan mengandung alphabet maupun numerik. Jika tidak, program akan mengeluarkan output "argumen hanya berupa alphabet".

```
now=$(date +%H)

echo $answer| tr $(printf %${now}s | tr ' ' '.')\A-Z A-ZA-Z | tr $(printf %${now}s | tr ' ' '.')\a-z a-za-z > /home/afif/sisop/mod/afif.txt
```
Untuk mengecek jam pada saat pembuatan file password tersebut dan men-generate nama untuk file password (harus terdiri dari a-z dan A-Z) dan disimpan pada sebuah file untuk sementara.

```
num=$(cat /home/afif/sisop/mod/afif.txt)
```
Mengambil data dari file kemudian dimasukkan ke dalam sebuah variabel.

```
mv  /home/afif/sisop/mod/$answer.txt /home/afif/sisop/mod/$num.txt
```
Rename nama file awal menggunakan enkripsi yang sudah dibuat pada proses sebelumnya

```
rm /home/afif/sisop/mod/afif.txt
```
Untuk menghapus file sementara yang menyimpan nama file enkripsi

