# Uas Database : mysql
Membuat database dengan MySQL

## Soal
 1. Buatlah database dengan nama Perkuliahan, Buatlah tabel-tabel berikut.<br>
	 a). Tabel mahasiswa, dengan struktur tabel sbb.
		 
    |Nama kolom|Type  | ket|
    |--|--|--|
    |kdmhs |varchar(10)  | Primary key |
    |nama_mhs | varchar(30) | not null |
    |alamat | varchar(50) | not null |
    |jk | char(1) | not null |
    |tgl_lahir | date | not null|
    
	b). Tabel matakuliah, dengan struktur tabel sbb.
    | Nama Kolom | Type | Ket |
    |--|--|--|
    | id_mtk | varchar(3) | primary key |
    | nama_mtk | varchar(30) | not null |
    |sks|int|not null|
    |semester|int|not null|
    
	c). Tabel nilai, degnan struktur tabel sbb.
    | Nama Kolom | Type | Ket |
    |--|--|--|
    | kdmhs | varchar(10) | foreign key |
    |id_mtk|varchar(3)|foreign key|
    |nilai|int|not null|
    
 2. Buatlah ERD sesuai Database diatas.
 3. Tambahkan <br>
   a). Foreign key di tabel nilai untuk kolom id_mtk reference id_mtk di tabel matakuliah, dan<br>
   b). Foreign key di tabel nilai untuk kolom kdmhs reference kdmhs di tabel mahasiswa.
 4. Tambahkan data data dalam tabel mahasiswa sbb. <br>
    |kdmhs|nama_mhs|alamat|jk|tgl_lahir|
    |--|--|--|--|--|
    |11001|Andi Mardan|Selong|L|2000-02-12|
    |12013|Suparman|Sakra|L|2001-08-10|
    |10202|Jonny Deep|Rensing|L|2000-03-11|
    |12501|Umi Nafisa|Labuhan|P|1998-01-9-20|
    |23300|Laili Hayati|Pancor|P|1999-02-21|
    
    Tambahkan data data dalam tabel matakuliah sbb.<br>
    |id_mtk|nama_mtk|sks|semester|
    |--|--|--|--|
    |MK1|Database|3|3|
    |MK2|Pemrograman Web|2|3|
    |MK3|Statistik|3|3|
    
    Tambahkan data data tabel dalam tabel tblNilai sbb.<br>
    |kdmhs|id_mtk|nilai|
    |--|--|--|
    |11001|MK1|80|
    |12013|MK1|60|
    |10202|MK2|75|
    |12501|MK2|90|
    |23300|MK3|77|
    |12013|MK3|88|
    |11001|MK3|60|
    |10202|MK1|55|
    |12501|MK3|75|
    |23300|MK1|65|
 5. Dengan perintah SQL jalankan dengan syntax yang benar query.
	 a). Tampilkan data mahasiswa yang memiliki usia lebih dari 20.<br>
	 b). Tampilkandata dalam table mahasiswa yang nama mahasiswa mengandung huruf 'u'.<br>
	 c). Tampilkan data nama mahasiswa secara DESCENDING dalam tabel mahasiswa.<br>
	 d). Tampilkan minimal usia mahasiswa dalam tabel mahasiswa.<br>
	 e). Tampilkan maksimal nilai yang ada dalam tabel nilai.<br>
	 f). Tampilkan rata-rata nilai seluruh mahasiswa.
## Jawab

 1. a). `CREATE TABLE mahasiswa(kdmhs VARCHAR(10) PRIMARY KEY, nama_mhs VARCHAR(30) NOT NULL, alamat VARCHAR(50) NOT NULL, jk CHAR(1) NOT NULL, tgl_lahir INT NOT NULL);`<br>
    b). `CREATE TABLE matakuliah(id_mtk VARCHAR(3) PRIMARY KEY, nama_mtk VARCHAR(30) NOT NULL, sks INT NOT NULL, semester INT NOT NULL);`<br>
    c). `CREATE TABLE tblNilai(kdmhs VARCHAR(10), id_mtk VARCHAR(3), nilai INT NOT NULL, FOREIGN KEY (kdmhs) REFERENCES mahasiswa(kdmhs), FOREIGN KEY (id_mtk) REFERENCES matakuliah(id_mtk));` 
 2. null
 3. ERD Perkuliahan. <br><br>
    ![ERD Perkuliahan](https://github.com/bayiPetani/kuliah/blob/main/images/erd.png)
 4. a). `INSERT INTO mahasiswa VALUES ('11001', 'Andi Mardian', 'Selong', 'L', '2000-02-12'), ('12013', 'Suparman', 'Sakra', 'L', '2001-08-10'), ('10202', 'Jonny Deep', 'Rensing', 'L', '2000-03-11'), ('12501', 'Umi Nafisa', 'Labuhan', 'P', '1998-01-20'), ('23300', 'Lalih Hayati', 'Pancor', 'P', '1999-02-21');` <br>
    b). `INSERT INTO matakuliah VALUES ('MK1', 'Database', 3, 3), ('MK2', 'Pemrograman Web', 2, 3), ('MK3', 'Statistik', 3, 3);`<br>
    c). `INSERT INTO tblNilai VALUES ('11001', 'MK1', 80), ('12013', 'MK1', 60), ('10202', 'MK2', 75), ('12501', 'MK2', 90), ('23300', 'MK3', 77), ('12013', 'MK3', 88), ('11001', 'MK3', 60), ('10202', 'MK1', 55), ('12501', 'MK3', 75), ('23300', 'MK1', 65);`
 5. Dengan perintah SQL jalankan dengan syntax yang benar query.<br>
	 a). `SELECT *, TIMESTAMPDIFF(YEAR, tgl_lahir, CURDATE()) AS umur FROM mahasiswa WHERE TIMESTAMPDIFF(YEAR, tgl_lahir, CURDATE()) > 20;`<br>
	 b). `SELECT * FROM mahasiswa WHERE INSTR(nama_mhs, 'u');`<br>
	 c). `SELECT * FROM mahasiswa ORDER BY nama_mhs DESC;`<br>
	 d).  `SELECT *, TIMESTAMPDIFF(YEAR, tgl_lahir, CURDATE()) AS umur FROM mahasiswa WHERE tgl_lahir=(SELECT MAX=(tgl_lahir) FROM mahasiswa);`<br>
	 e). `SELECT * FROM tblNilai WHERE nilai=(SELECT MAX(nilai) FROM tblNilai);`<br>
	 f). `SELECT AVG(nilai) FROM tblNilai;`
