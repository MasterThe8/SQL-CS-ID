# SQL Fundamentals
*owner : MasterThe8*

---
## Manipulation
Operasi-operasi yang digunakan untuk memanipulasi data dalam basis data.

### CREATE
Membuat tabel

```
CREATE TABLE table_name (
  column1 datatype,
  column2 datatype,
  column3 datatype
);
```

### INSERT
Menambah data (baris) baru ke tabel

```
-- Insert into columns in order:
INSERT INTO table_name
VALUES (value1, value2);

-- Insert into columns by name:
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

### ALTER
`ALTER TABLE` digunakan untuk mengubah kolom tabel yang ada. Jika digabungkan dengan klausa `ADD`, digunakan untuk menambahkan kolom baru.

```
ALTER TABLE table_name
ADD column_name datatype;
```

### DELETE
Menghapus baris pada tabel
```
DELETE FROM table_name
WHERE some_column = some_value;
```

### UPDATE
Memperbarui value pada tabel berdasarkan baris
```
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE some_column = some_value;

-- Example:
UPDATE Customers
SET ContactName = 'Asuka', City = 'Tokyo'
WHERE CustomerID = 1;
```
---
## Queries
Operasi-operasi (Query) yang digunakan untuk mengambil data dari basis data.

### AND
Operator `AND` memungkinkan beberapa kondisi untuk digabungkan.
```
SELECT model 
FROM cars 
WHERE color = 'blue' 
  AND year > 2014;
```

### AS
Kolom atau tabel dapat diberi alias menggunakan klausa `AS`. Hal ini memungkinkan kolom atau tabel diganti namanya secara khusus di kumpulan hasil yang dikembalikan. Kueri yang diberikan akan mengembalikan kumpulan hasil dengan kolom `name` diubah namanya menjadi `movie_title`.
```
SELECT name AS 'movie_title'
FROM movies;
```

### OR
Operator `OR` memungkinkan beberapa kondisi untuk digabungkan. Rekaman yang cocok dengan salah satu kondisi yang digabungkan dengan `OR` disertakan dalam kumpulan hasil.
```
SELECT name
FROM customers 
WHERE state = 'CA' 
   OR state = 'NY';
```

### `%` and `_` Wildcard
Wildcard adalah karakter khusus yang digunakan untuk mencocokkan pola dalam string saat melakukan pencarian atau filtering data.
- `%` (persentase): Digunakan untuk mencocokkan nol atau lebih karakter apa pun dalam string.
- `_` (garis bawah): Digunakan untuk mencocokkan satu karakter tunggal dalam string.

```
SELECT * FROM customers WHERE name LIKE 'J%'
```
akan mencocokkan semua nama yang dimulai dengan huruf 'J'.
```
SELECT * FROM products WHERE name LIKE '%apple%'
```
akan mencocokkan semua produk yang memiliki kata 'apple' di dalam namanya.
```
SELECT * FROM employees WHERE last_name LIKE '_mith'
```
akan mencocokkan semua nama belakang yang memiliki lima karakter, di mana karakter keempat adalah 'm' dan karakter terakhir adalah 'i', 't', dan 'h'.

### ORDER BY
Klausa `ORDER BY` dapat digunakan untuk mengurutkan hasil yang ditetapkan berdasarkan kolom tertentu baik berdasarkan abjad atau numerik. Itu dapat dipesan dengan dua cara:

- `DESC` adalah kata kunci yang digunakan untuk mengurutkan hasil dalam urutan menurun.
- `ASC` adalah kata kunci yang digunakan untuk mengurutkan hasil dalam urutan menaik (default).

```
SELECT * FROM customers ORDER BY last_name ASC;

SELECT * FROM products ORDER BY price DESC;

SELECT * FROM orders ORDER BY order_date DESC, total_amount ASC;
```

### GROUP BY
Klausa `GROUP BY` digunakan untuk mengelompokkan baris berdasarkan nilai dalam satu atau beberapa kolom. Ketika Anda menggunakan `GROUP BY`, setiap baris dalam hasil query akan dikelompokkan berdasarkan nilai yang sama dalam kolom yang ditentukan.
```
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```
Pernyataan ini akan menghitung jumlah pegawai dalam setiap departemen dengan menggunakan GROUP BY department.

```
SELECT rating, 
   COUNT(*) 
FROM movies 
GROUP BY rating;
```

### LIKE
Operator `LIKE` dapat digunakan di dalam klausa `WHERE` untuk mencocokkan pola tertentu.

- `%` (persentase): Cocokkan nol atau lebih karakter.
- `_` (garis bawah): Cocokkan satu karakter tunggal.

Pada contoh ini, query akan mengembalikan semua produk yang memiliki kata 'apple' di dalam nama produknya.
```
SELECT * FROM products WHERE name LIKE '%apple%';
```

Pada contoh ini, query akan mengembalikan semua pelanggan yang memiliki alamat email dengan domain 'gmail.com', dengan satu karakter sebelum karakter '@'.
```
SELECT * FROM customers WHERE email LIKE '_@gmail.com';
```

Pada contoh ini, query akan mengembalikan semua pegawai yang nama belakangnya dimulai dengan huruf 'Sm'.
```
SELECT * FROM employees WHERE last_name LIKE 'Sm%';
```

### DISTINCT
Klausa `DISTINCT` digunakan untuk menghapus duplikat dari hasil query sehingga hanya nilai unik yang ditampilkan.

```
SELECT DISTINCT department FROM employees;
```
Pada contoh di atas, query akan mengembalikan daftar departemen unik dari tabel "employees", menghilangkan duplikat. Ini berguna jika Anda ingin melihat departemen apa saja yang ada di perusahaan tanpa adanya duplikat.

```
SELECT DISTINCT first_name, last_name FROM customers;
```
Pada contoh ini, query akan mengembalikan daftar nama pelanggan unik dari tabel "customers", tanpa adanya duplikat. Ini memungkinkan Anda untuk melihat kombinasi unik dari nama pelanggan dalam tabel.

### BETWEEN
Operator `BETWEEN` digunakan untuk memfilter hasil query berdasarkan range nilai tertentu dari sebuah kolom. Operator ini memungkinkan Anda untuk menentukan batas atas dan batas bawah yang ingin Anda sertakan dalam pencarian.

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
- `column_name` adalah nama kolom yang akan diuji.
- `value1` dan `value2` adalah nilai yang menentukan batas bawah dan batas atas dari range yang ingin Anda cari.

```
SELECT * FROM products
WHERE price BETWEEN 10 AND 20;
```
Pada contoh ini, query akan mengembalikan semua produk dengan harga antara 10 dan 20.

### LIMIT
Klausa `LIMIT` digunakan untuk membatasi jumlah baris yang dikembalikan oleh sebuah query. Ini sangat berguna ketika Anda ingin mengambil sejumlah tertentu dari hasil query, terutama jika tabel tersebut memiliki banyak baris dan Anda hanya memerlukan sebagian kecil dari hasilnya.

```
SELECT * FROM products
LIMIT 10;
```
Pada contoh ini, query akan mengembalikan 10 produk pertama dari tabel "products".

```
SELECT * FROM employees
LIMIT 5, 10;
```
Pada contoh ini, query akan mengembalikan 10 pegawai dimulai dari baris ke-6 (karena pengindeksan dimulai dari 0) dalam tabel "employees". `5` adalah offset, yang menunjukkan mulai dari baris ke-6, dan `10` adalah jumlah baris yang akan diambil setelah offset tersebut.

### NULL
NULL adalah nilai yang menunjukkan bahwa kolom tidak memiliki nilai data yang valid.

Beberapa hal yang perlu diingat tentang nilai NULL:

- NULL tidak sama dengan 0 atau string kosong ('').
- Kondisi yang melibatkan nilai NULL menggunakan operator `IS NULL` atau `IS NOT NULL` karena NULL tidak dapat diuji dengan operator perbandingan seperti `=`, `!=`, `<`, `>`, dll.
- Ketika Anda membandingkan nilai dengan NULL, hasilnya selalu NULL.
- NULL dianggap tidak sama dengan NULL dalam kondisi perbandingan.
- Ketika NULL muncul dalam ekspresi matematika, hasilnya selalu NULL.
- Dalam tabel, kolom yang dideklarasikan dengan jenis data tertentu dapat berisi NULL jika kolom tersebut dibiarkan kosong atau jika data yang dimasukkan tidak valid.

```
SELECT * FROM employees WHERE department IS NULL;
```
Query ini akan mengembalikan semua pegawai yang tidak terdaftar dalam departemen manapun, karena kolom departemen mereka berisi nilai NULL.

```
SELECT * FROM students WHERE score IS NOT NULL;
```
Query ini akan mengembalikan semua siswa yang memiliki nilai tidak NULL dalam kolom "score", yaitu siswa yang telah menerima penilaian.

---

## Aggregate Functions
Fungsi-fungsi yang digunakan untuk melakukan operasi agregasi pada sekelompok nilai.

### SUM()
Fungsi `SUM()` digunakan untuk menjumlahkan nilai numerik dari suatu kolom dalam hasil query.

```
transaction_id | amount
1              | 100.00
2              | 150.00
3              | 75.00
4              | 200.00
5              | 80.00
```
```
SELECT SUM(amount) AS total_sales
FROM sales;
```
```
total_sales
605.00
```

### MAX()
Fungsi `MAX()` digunakan untuk mengambil nilai maksimum dari sebuah kolom dalam hasil query.

```
product_id | product_name | price
1          | Laptop       | 1200.00
2          | Smartphone   | 800.00
3          | Tablet       | 500.00
4          | Headphones   | 150.00
5          | Mouse        | 30.00
```
```
SELECT MAX(price) AS highest_price
FROM products;
```
```
highest_price
1200.00
```

### MIN()
Fungsi `MIN()` digunakan untuk mengambil nilai minimum dari sebuah kolom dalam hasil query.

```
product_id | product_name | price
1          | Laptop       | 1200.00
2          | Smartphone   | 800.00
3          | Tablet       | 500.00
4          | Headphones   | 150.00
5          | Mouse        | 30.00
```
```
SELECT MIN(price) AS lowest_price
FROM products;
```
```
lowest_price
30.00
```

### COUNT()
Fungsi `COUNT()` digunakan untuk menghitung jumlah baris atau nilai yang ditemukan dalam sebuah kolom atau hasil query.

- Menghitung jumlah baris dalam sebuah tabel:
```
SELECT COUNT(*) AS total_rows
FROM employees;
```
Hasilnya akan memberikan jumlah total baris dalam tabel "employees".

- Menghitung jumlah nilai yang tidak NULL dalam sebuah kolom:
```
SELECT COUNT(salary) AS total_salaries
FROM employees;
```
Hasilnya akan memberikan jumlah total nilai gaji yang tidak NULL dalam kolom "salary" pada tabel "employees".

- Menggunakan COUNT() bersama dengan GROUP BY untuk menghitung jumlah baris dalam setiap kelompok:
```
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```
Hasilnya akan memberikan jumlah total pegawai dalam setiap departemen dalam tabel "employees".

### AVG()
Fungsi `AVG()` digunakan untuk menghitung nilai rata-rata dari suatu kolom numerik dalam hasil query. 
```
student_id | grade
1          | 85
2          | 92
3          | 78
4          | 90
5          | 88
```
```
SELECT AVG(grade) AS average_grade
FROM grades;
```
```
average_grade
86.6
```

### ROUND()
Fungsi `ROUND()` digunakan untuk membulatkan nilai numerik ke jumlah digit yang ditentukan setelah titik desimal.
```
ROUND(numeric_expression, num_decimal_places)
```
- `numeric_expression` adalah nilai numerik yang ingin dibulatkan.
- `num_decimal_places` adalah jumlah digit desimal yang diinginkan setelah pembulatan.

Example:
```
SELECT ROUND(123.456, 2) AS rounded_number;
```
Pada contoh ini, nilai numerik 123.456 akan dibulatkan menjadi dua digit desimal setelah titik desimal, sehingga hasilnya adalah 123.46.

```
SELECT ROUND(5.6789, 1) AS rounded_number;
```
Pada contoh ini, nilai numerik 5.6789 akan dibulatkan menjadi satu digit desimal setelah titik desimal, sehingga hasilnya adalah 5.7.

### HAVING
Klausa `HAVING` digunakan bersama dengan klausa `GROUP BY` dalam pernyataan SQL untuk memberikan kondisi filter pada hasil dari pengelompokan yang dihasilkan oleh `GROUP BY`. Ini berarti Anda dapat menggunakan `HAVING` untuk menerapkan kondisi pada hasil agregat yang dihasilkan oleh pengelompokan, mirip dengan cara Anda menggunakan klausa `WHERE` untuk menerapkan kondisi pada baris-baris individual dalam hasil query.

Misalkan kita memiliki tabel "orders" yang berisi daftar pesanan beserta total harga dari setiap pesanan, dan kita ingin mengelompokkan pesanan berdasarkan ID pelanggan dan hanya menampilkan pelanggan yang memiliki total pembelian lebih dari 1000:
```
SELECT customer_id, SUM(total_price) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(total_price) > 1000;
```
Pada contoh di atas, klausa `GROUP BY customer_id` digunakan untuk mengelompokkan pesanan berdasarkan ID pelanggan. Kemudian, klausa `HAVING` digunakan untuk memfilter hasil pengelompokan tersebut, sehingga hanya menampilkan pelanggan yang total pembelian mereka melebihi 1000.

Perlu diingat bahwa `HAVING` digunakan setelah `GROUP BY` dan sebelum `ORDER BY` dalam sebuah pernyataan SQL. Ini memungkinkan Anda untuk menerapkan kondisi pada hasil agregat, sementara `WHERE` diterapkan pada baris individual sebelum dilakukan pengelompokan.

---
## Multiple Tables
Kueri yang melibatkan beberapa tabel seringkali digunakan untuk mengambil data yang berkaitan dari beberapa sumber data.

### Outer Join
Outer Join adalah operasi join yang menggabungkan baris dari dua tabel berdasarkan kriteria yang ditentukan dan juga memasukkan baris yang tidak memiliki kecocokan dari kedua tabel.

Ada tiga jenis Outer Join:

- **Left Outer Join (atau Left Join)**: Mengembalikan semua baris dari tabel kiri (tabel yang disebut pertama dalam pernyataan JOIN), dan baris yang cocok dari tabel kanan (tabel kedua yang disebut) jika ada.

Misalkan kita memiliki dua tabel: "customers" dan "orders". Kita ingin menggabungkan data dari kedua tabel sehingga kita dapat melihat informasi pelanggan bersama dengan pesanan mereka, bahkan jika ada pelanggan yang belum membuat pesanan.
```
SELECT customers.customer_id, customers.name, orders.order_id, orders.order_date
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```

- **Right Outer Join (atau Right Join)**: Mengembalikan semua baris dari tabel kanan, dan baris yang cocok dari tabel kiri jika ada.

Misalkan kita memiliki dua tabel: "customers" dan "orders". Kita ingin menggabungkan data dari kedua tabel sehingga kita dapat melihat informasi pesanan bersama dengan informasi pelanggan yang telah membuat pesanan, bahkan jika ada pesanan yang tidak memiliki informasi pelanggan yang terkait.
```
SELECT customers.customer_id, customers.name, orders.order_id, orders.order_date
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.customer_id;
```

- **Full Outer Join (atau Full Join)**: Mengembalikan semua baris dari kedua tabel, mencocokkan baris jika ada dan memasukkan baris yang tidak memiliki kecocokan dari kedua tabel

Misalkan kita ingin menggabungkan data dari dua tabel "customers" dan "orders" sehingga kita dapat melihat semua informasi pelanggan bersama dengan semua pesanan, bahkan jika ada pelanggan yang tidak memiliki pesanan atau pesanan yang tidak memiliki informasi pelanggan yang terkait.
```
SELECT customers.customer_id, customers.name, orders.order_id, orders.order_date
FROM customers
FULL JOIN orders ON customers.customer_id = orders.customer_id;
```

### Inner Join
Inner Join adalah salah satu jenis operasi join dalam SQL yang menggabungkan baris dari dua tabel berdasarkan kriteria yang ditentukan dan hanya mengembalikan baris yang memiliki kecocokan dalam kedua tabel. Dengan kata lain, Inner Join menggabungkan baris dari kedua tabel hanya jika ada nilai yang cocok di kolom yang dijadikan sebagai kunci penggabungan.

Misalkan kita memiliki dua tabel: "customers" dan "orders". Tabel "customers" berisi informasi pelanggan, sedangkan tabel "orders" berisi informasi pesanan yang dilakukan oleh pelanggan.
```
SELECT customers.customer_id, customers.name, orders.order_id, orders.order_date
FROM customers
INNER JOIN orders ON customers.customer_id = orders.customer_id;
```
Pada contoh ini, Inner Join digunakan untuk menggabungkan informasi dari kedua tabel berdasarkan kolom "customer_id". Hasilnya adalah hanya baris-baris di mana ada pelanggan yang memiliki pesanan yang cocok akan ditampilkan. Jika tidak ada pesanan yang cocok untuk seorang pelanggan, baris tersebut tidak akan dimasukkan dalam hasilnya.

### Cross Join
Cross Join adalah jenis operasi join dalam SQL yang menggabungkan setiap baris dari satu tabel dengan setiap baris dari tabel lainnya, tanpa memperhatikan kondisi penggabungan tertentu. Dengan kata lain, Cross Join menghasilkan hasil gabungan dari kedua tabel, di mana setiap baris dari tabel pertama dikombinasikan dengan setiap baris dari tabel kedua.

Misalkan kita memiliki dua tabel: "customers" dan "products". Tabel "customers" berisi daftar pelanggan, sedangkan tabel "products" berisi daftar produk.
```
SELECT customers.customer_id, customers.name, products.product_id, products.product_name
FROM customers
CROSS JOIN products;
```
Pada contoh ini, Cross Join akan menghasilkan hasil gabungan dari setiap baris dalam tabel "customers" dengan setiap baris dalam tabel "products". Ini berarti setiap pelanggan akan dikombinasikan dengan setiap produk, menghasilkan setiap kemungkinan pasangan pelanggan-produk. Jumlah baris dalam hasilnya akan menjadi jumlah baris dalam tabel "customers" dikalikan dengan jumlah baris dalam tabel "products".

### WITH
Klausa `WITH` digunakan untuk membuat satu atau beberapa tabel sementara yang dapat digunakan dalam query utama.

Misalkan kita memiliki tabel "employees" dan kita ingin membuat query yang menggabungkan informasi tentang pegawai bersama dengan informasi tentang departemen mereka, tetapi kita ingin menggunakannya dalam beberapa bagian dari query.
```
WITH EmployeeDepartments AS (
    SELECT e.employee_id, e.employee_name, d.department_name
    FROM employees e
    JOIN departments d ON e.department_id = d.department_id
)
SELECT ed.employee_id, ed.employee_name, ed.department_name, COUNT(*) AS num_employees
FROM EmployeeDepartments ed
GROUP BY ed.department_name;
```
Dalam contoh ini, kita menggunakan `WITH` untuk membuat CTE yang disebut "EmployeeDepartments" yang menggabungkan informasi pegawai dengan informasi departemen. Kemudian, kita menggunakan CTE tersebut dalam query utama untuk menghitung jumlah pegawai dalam setiap departemen. Ini membuat query lebih mudah dibaca dan lebih mudah dimengerti.

### UNION
Klausa `UNION` digunakan untuk menggabungkan hasil dua atau lebih query yang memiliki struktur dan tipe data yang sama menjadi satu hasil tunggal. Hasil `UNION` akan menghilangkan duplikat dari hasil penggabungan.

```
SELECT employee_name AS name
FROM employees
UNION
SELECT customer_name AS name
FROM customers;
```
Dalam contoh ini, kita menggunakan UNION untuk menggabungkan nama-nama pegawai dari tabel "employees" dengan nama-nama pelanggan dari tabel "customers". Hasilnya adalah satu daftar tunggal yang berisi semua nama, di mana duplikat akan dihapus.

Penting untuk diingat bahwa untuk menggunakan UNION, jumlah dan tipe data kolom yang dihasilkan oleh kedua subquery harus sama atau sesuai. Jika jumlah atau tipe data kolom tidak cocok, query akan menghasilkan kesalahan.

### PRIMARY KEY
Primary Key adalah satu atau sekelompok kolom dalam sebuah tabel yang secara unik mengidentifikasi setiap baris atau catatan dalam tabel tersebut.
- Setiap tabel harus memiliki satu Primary Key, yang mengidentifikasi baris-baris unik dalam tabel tersebut.
- Nilai dalam kolom Primary Key harus unik dan tidak boleh NULL.
- Primary Key sering kali diterapkan dengan menggunakan indeks, yang mempercepat pencarian dan pengindeksan data.
- Contoh: Jika kita memiliki tabel "students" dengan kolom "student_id" sebagai Primary Key, setiap nilai dalam kolom "student_id" harus unik dan dapat mengidentifikasi setiap siswa dengan cara yang eksklusif.
```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    customer_email VARCHAR(100)
);
```

### FOREIGN KEY
Foreign Key adalah satu atau sekelompok kolom dalam sebuah tabel yang merujuk ke Primary Key atau Unique Key di tabel lain.
- Foreign Key menciptakan hubungan antara dua tabel, memungkinkan tabel untuk saling terkait dalam basis data.
- Foreign Key digunakan untuk menerapkan integritas referensial, yang memastikan bahwa nilai dalam kolom yang mengacu ke tabel lain selalu memiliki referensi yang valid.
- Nilai dalam kolom Foreign Key bisa saja NULL, yang berarti tidak ada referensi yang valid.
- Contoh: Jika kita memiliki tabel "orders" dengan kolom "customer_id" sebagai Foreign Key yang merujuk ke kolom "customer_id" dalam tabel "customers", maka setiap nilai dalam kolom "customer_id" dalam tabel "orders" harus ada dalam kolom "customer_id" dalam tabel "customers".
```
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```