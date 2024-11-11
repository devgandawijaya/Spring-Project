# Database Schema

## 1. Tabel `users`
Tabel ini menyimpan informasi pengguna seperti email, password, nomor telepon, KTP, saldo, dan waktu pembuatan/pembaruan data pengguna.

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    telp VARCHAR(20),
    ktp VARCHAR(20),
    balance DECIMAL(10, 2) DEFAULT 0.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE lockers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    rental_price DECIMAL(10, 2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE history (
    id SERIAL PRIMARY KEY,
    id_user INT NOT NULL,
    amount DECIMAL(10, 2) NOT NULL,
    type VARCHAR(50) CHECK (type IN ('topup', 'payment', 'refund')) NOT NULL,
    note TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_user) REFERENCES users(id)
);

CREATE TABLE history (
    id SERIAL PRIMARY KEY,
    id_user INT NOT NULL,
    amount DECIMAL(10, 2) NOT NULL,
    type VARCHAR(50) CHECK (type IN ('topup', 'payment', 'refund')) NOT NULL,
    note TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_user) REFERENCES users(id)
);

CREATE TABLE setting (
    id SERIAL PRIMARY KEY,
    late_charge DECIMAL(10, 2) DEFAULT 10000.00
);

CREATE TABLE key_error_logger (
    id SERIAL PRIMARY KEY,
    booking_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

