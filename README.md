## Profil
| Variable | Isi |
| -------- | --- |
| **Nama** | ANDIKA SETIAWAN |
| **NIM** | 312310470 |
| **Kelas** | TI.23.A5 |
| **Mata Kuliah** | Basis data |

# Soal Latihan Praktikum
## Data Model Mapping

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```
- Buat DDL Script berdasarkan skema ERD tersebut diatas. 
- Jalankan script DDL tersebut pada DBMS MySQL.

**Langkah-langkahnya :**

**1. Buat dulu script untuk table Mahasiswa :**

```
create table Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```
![alt text](FOTO/gambar1.png)
**Tampilkan hasil table :**

`desc Mahasiswa;`
![alt text](FOTO/gambar2.png)

**2. Buat script untuk table Dosen :**
```
create table Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );
```
![alt text](FOTO/gambar3.png)

**Tampilkan tabel :**

`desc Dosen;`

![alt text](FOTO/gambar4.png)

**3. Buat script untuk Mata kuliah :**
```
create table Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );
```

![alt text](FOTO/gambar5.png)

**Tampilkan table :**

`desc Matakuliah;`

![alt text](FOTO/gambar6.png)

**4. Buat script untuk jadwal mengajar :**
```
create table JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    ); 
```

![alt text](FOTO/gambar7.png)

**Tampilkan table :**

`desc JadwalMengajar;`
![alt text](FOTO/gambar8.png)

**5. Buat script untuk KRSMahasiswa :**
```
CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

![alt text](FOTO/gambar9.png)

**Tampilkan table :**


![alt text](FOTO/gambar10.png)

# Soal Latihan Praktikum

Berdasarkan table Mahasiswa pada praktikum sebelumnya: (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

***Isi data pada table tersebut sebanyak minimal 5 record data. Tampilkan semua isi/record tabel!***

- Ubah data tanggal lahir Mahasiswa yang bernama Ari menjadi: 1979-08-31!

- Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!

- Hapus Mahasiswa yang bernama Dina!

- Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!

- Tampilkan data nama dan alamat Mahasiswa saja dari tabel tersebut

- Tampilkan data Mahasiswa terurut berdasarkan nama.

**1. Mengisi tabel dengan minimal 5 record data :**
```
insert into Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");
```
![alt text](FOTO/gambar11.png)
**2. Menampilkan semua isi/record pada tabel bisa menggunakan kode berikut :**

`select*from Mahasiswa;`
![alt text](FOTO/gambar12.png)
**3. Mengubah data tanggal lahir Mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :**

`update Mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;`
![alt text](FOTO/gambar13.png)
**4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :**

`select*from Mahasiswa where nim=11223344;`
![alt text](FOTO/gambar14.png)
**5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:**

`delete from Mahasiswa where nim=11223346;`
![alt text](FOTO/gambar15.png)
**6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :**

`select*from Mahasiswa where tgl_lahir<='1996-1-2';`
![alt text](FOTO/gambar16.png)
**7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :**

`select*from Mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';`
![alt text](FOTO/gambar17.png)
**8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :**
```
select * from Mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' 
or tgl_lahir<='2002-4-22' 
and jenis_kelamin='Perempuan';
```
![alt text](FOTO/gambar18.png)
**9. Menampilkan data nama dan jalan Mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :**

`select nama, jalan from Mahasiswa;`
![alt text](FOTO/gambar19.png)
**10. Menampilkan data Mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :**

`select*from Mahasiswa -> order by nama asc;`
![alt text](FOTO/gambar20.png)
# Evaluasi dan Pertanyaan

***Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!***

**1. Menambah data :**

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

`INSERT INTO Mahasiswa (nim, nama, alamat) VALUE ('1234','Andika','Cikarang');`
![alt text](FOTO/gambar21.png)
**2. Menampilkan data :**

`SELECT * FROM <table> SELECT [field1, ..., fieldn] FROM <table>`

`SELECT*FROM Mahasiswa;`
![alt text](FOTO/gambar22.png)
**3. Mengubah data :**

`UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>;`

*Contoh :*

`UPDATE Mahasiswa SET nama='Setiawan', alamat='Kota Serang Baru' WHERE nim='1234';`
![alt text](FOTO/gambar23.png)
**4. Menghapus data :**

`DELETE FROM <table> WHERE <kondisi>`

*Contoh :*

`DELETE FROM Mahasiswa WHERE nim=‘1234’`
![alt text](FOTO/gambar24.png)
***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

**Jawaban nya :**

Operator BETWEEN ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan untuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>

***Berikan kesimpulan anda!***

Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekkan diatas.

***Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen.***

***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

**Jawaban nya :**

Operator BETWEEN ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan untuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>

***Berikan kesimpulan anda!***

Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekkan diatas.

***Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen.***