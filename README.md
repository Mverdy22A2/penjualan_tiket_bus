# ER-D

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/dd0c266b-b4e5-42a2-8cd6-a8bb45248f6b)

## table armada

    CREATE TABLE Armada (
    armada_id INT PRIMARY KEY,
    nama_armada VARCHAR(255)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/84c902b0-495d-4136-b3f4-f748c0762480)

## table jadwal berangkat

    CREATE TABLE JadwalBerangkat (
    jadwal_id INT PRIMARY KEY,
    armada_id INT,
    tanggal_keberangkatan DATE,
    jam_keberangkatan TIME,
    FOREIGN KEY (armada_id) REFERENCES Armada(armada_id)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/422b1db3-0121-43f1-807d-6b7a793cdafc)

## table penumpang

    CREATE TABLE Penumpang (
    penumpang_id INT PRIMARY KEY,
    nama_penumpang VARCHAR(255),
    alamat VARCHAR(255),
    no_telepon VARCHAR(20),
    posisi_tempat_duduk VARCHAR(10)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/67ef10ed-715a-45c0-b884-8d360881d3bb)

## table transaksi

    CREATE TABLE Transaksi (
    transaksi_id INT PRIMARY KEY,
    jadwal_id INT,
    penumpang_id INT,
    harga DECIMAL(10,2),
    tanggal_beli DATE,
    FOREIGN KEY (jadwal_id) REFERENCES JadwalBerangkat(jadwal_id),
    FOREIGN KEY (penumpang_id) REFERENCES Penumpang(penumpang_id)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/85e983cd-51f5-44dd-8559-4858e4aa45d2)

# SQL CRUD

## 1. armada

    -- Create
    INSERT INTO Armada (armada_id, nama_armada) VALUES (1, 'Armada A');
    INSERT INTO Armada (armada_id, nama_armada) VALUES (2, 'Armada B');

    -- Read
    SELECT * FROM Armada;

    -- Update
    UPDATE Armada SET nama_armada = 'Armada C' WHERE armada_id = 1;

    -- Delete
    DELETE FROM Armada WHERE armada_id = 2;

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/6476e784-828e-4c3e-9d14-e2797fc85570)

## 2. jadwalberangkat

    -- Create
    INSERT INTO JadwalBerangkat (jadwal_id, armada_id, tanggal_keberangkatan, jam_keberangkatan)
    VALUES (1, 1, '2023-06-19', '08:00:00');
    INSERT INTO JadwalBerangkat (jadwal_id, armada_id, tanggal_keberangkatan, jam_keberangkatan)
    VALUES (2, 2, '2023-06-20', '09:30:00');

    -- Read
    SELECT * FROM JadwalBerangkat;

    -- Update
    UPDATE JadwalBerangkat SET jam_keberangkatan = '10:00:00' WHERE jadwal_id = 1;

    -- Delete
    DELETE FROM JadwalBerangkat WHERE jadwal_id = 2;

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/9b03a6a0-0e21-4eaf-b3f5-5e9b99d273d7)

## 3. penumpang

        -- Create
        INSERT INTO Penumpang (penumpang_id, nama_penumpang, alamat, no_telepon, posisi_tempat_duduk)
        VALUES (1, 'John Doe', 'Jl. ABC No. 123', '081234567890', 'A1');
        INSERT INTO Penumpang (penumpang_id, nama_penumpang, alamat, no_telepon, posisi_tempat_duduk)
        VALUES (2, 'Jane Smith', 'Jl. XYZ No. 456', '089876543210', 'B2');

        -- Read
        SELECT * FROM Penumpang;

        -- Update
        UPDATE Penumpang SET no_telepon = '081111111111' WHERE penumpang_id = 1;

        -- Delete
        DELETE FROM Penumpang WHERE penumpang_id = 2;

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/61947dea-8d7e-407b-a391-a03e378441e8)

## 4. transaksi

        -- Create
        INSERT INTO Transaksi (transaksi_id, jadwal_id, penumpang_id, harga, tanggal_beli)
        VALUES (1, 1, 1, 50000.00, '2023-06-18');
        INSERT INTO Transaksi (transaksi_id, jadwal_id, penumpang_id, harga, tanggal_beli)
        VALUES (2, 2, 2, 75000.00, '2023-06-18');

        -- Read
        SELECT * FROM Transaksi;

        -- Update
        UPDATE Transaksi SET harga = 60000.00 WHERE transaksi_id = 1;

        -- Delete
        DELETE FROM Transaksi WHERE transaksi_id = 2;

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/e7bb6c88-e74d-4e40-9a28-f257427980bd)

# SQL JOIN

## Menggabungkan tabel JadwalBerangkat, Armada, dan Penumpang berdasarkan Transaksi
        SELECT t.transaksi_id, j.tanggal_keberangkatan, j.jam_keberangkatan, a.nama_armada,
        p.nama_penumpang, p.posisi_tempat_duduk, t.harga
        FROM Transaksi t
        JOIN JadwalBerangkat j ON t.jadwal_id = j.jadwal_id
        JOIN Armada a ON j.armada_id = a.armada_id
        JOIN Penumpang p ON t.penumpang_id = p.penumpang_id;


![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/e3240d5d-83f3-4db9-9cd5-acd95f83bc43)
