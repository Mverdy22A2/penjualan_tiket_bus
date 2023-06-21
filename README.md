# ER-D

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/55aa68fc-90cc-4647-b6e0-ce03518dc49c)

## table armada

    CREATE TABLE Armada (
    armada_id INT PRIMARY KEY,
    nama_armada VARCHAR(255)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/53e3445a-204f-48bb-8bb5-e03de077e3df)

## table jadwal berangkat

    CREATE TABLE JadwalBerangkat (
    jadwal_id INT PRIMARY KEY,
    armada_id INT,
    tanggal_keberangkatan DATE,
    jam_keberangkatan TIME,
    FOREIGN KEY (armada_id) REFERENCES Armada(armada_id)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/dd4bffa0-3997-4dd3-a484-1a3298fb739b)

## table penumpang

    CREATE TABLE Penumpang (
    penumpang_id INT PRIMARY KEY,
    nama_penumpang VARCHAR(255),
    alamat VARCHAR(255),
    no_telepon VARCHAR(20),
    posisi_tempat_duduk VARCHAR(10)
    );

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/74c10f3a-67ae-4669-95b1-93e426b78bc8)

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

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/d560d333-b783-464c-ba81-58079c48bd7c)

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

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/1f990b41-55f0-43a4-8f4b-effbe97d6d02)

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

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/0b0ba804-2f37-47b0-964c-23e50bcb5c0f)

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

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/44c8ca17-0737-4ed5-ba8b-d37962877297)

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

![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/fd7d8086-4f2b-41b1-b996-2f1e9b35f07d)

# SQL JOIN

## Menggabungkan tabel JadwalBerangkat, Armada, dan Penumpang berdasarkan Transaksi
        SELECT t.transaksi_id, j.tanggal_keberangkatan, j.jam_keberangkatan, a.nama_armada,
        p.nama_penumpang, p.posisi_tempat_duduk, t.harga
        FROM Transaksi t
        JOIN JadwalBerangkat j ON t.jadwal_id = j.jadwal_id
        JOIN Armada a ON j.armada_id = a.armada_id
        JOIN Penumpang p ON t.penumpang_id = p.penumpang_id;


![image](https://github.com/verz666/penjualan_tiket_bus/assets/115523263/3cbe7587-3182-49bd-ae90-fa810f0ed64a)
