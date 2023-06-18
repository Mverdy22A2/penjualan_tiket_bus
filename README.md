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

