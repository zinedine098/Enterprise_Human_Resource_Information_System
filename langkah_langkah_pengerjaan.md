Berikut versi **Markdown (MD)** yang sudah dirapikan, terstruktur, dan enak dibaca 👇

---

# 🧠 PHASE 0 – Planning

> ⚠️ **WAJIB — Jangan Skip Phase Ini**

---

## ✅ Step 1 – Tentukan Scope Final

Putuskan batasan awal sistem:

* Single company dulu
* Tanpa multi-tenant
* Tanpa recruitment module
* Fokus ke:

  * Employee
  * Attendance
  * Leave
  * Payroll

> 🎯 **Tujuan:** Jangan buat sistem terlalu besar di awal. Bangun pondasi yang solid dulu.

---

## ✅ Step 2 – Design ERD

Gunakan tools seperti:

* draw.io
* dbdiagram.io

### Yang harus dipastikan:

* ✔️ Foreign Key (FK)
* ✔️ Unique Constraint
* ✔️ Indexing

> 🧠 Ini melatih kamu berpikir sebagai **System Designer**, bukan hanya programmer.

---

# 🚀 PHASE 1 – Backend Foundation (Week 1–2)

---

## ✅ Step 3 – Setup Laravel Project

* Install Laravel
* Setup database
* Buat folder structure yang clean:

```bash
app/
 ├── Http/
 ├── Services/
 ├── Repositories/
 ├── Actions/
 ├── Policies/
```

> 🎯 Tujuan: Struktur rapi sejak awal = scalable di masa depan.

---

## ✅ Step 4 – Authentication System

* Install Sanctum
* Buat Login API
* Buat Register (HR only)
* Protect route dengan middleware
* Buat role middleware

### Latihan yang harus dikuasai:

* Policy
* Gate
* Role-based access

---

## ✅ Step 5 – Role & Permission System

Pilihan:

* Buat manual RBAC
* Atau gunakan `spatie/laravel-permission`

### Role Awal:

* Admin
* HR
* Manager
* Employee

---

# 🏢 PHASE 2 – Organization Structure (Week 3)

---

## ✅ Step 6 – Department Module

* CRUD department
* Support `parent_id` (hierarchy)
* API pagination

---

## ✅ Step 7 – Position Module

* CRUD position
* Tambahkan level jabatan

---

# 👨‍💼 PHASE 3 – Employee Module (Week 4–5)

> 🔥 Ini adalah core system.

---

## ✅ Step 8 – Employee CRUD

Relasi wajib:

* ke department
* ke position
* ke manager

---

## ✅ Step 9 – Upload Dokumen

* Gunakan Storage
* Validasi file
* Simpan path di database

---

## ✅ Step 10 – Salary Structure

⚠️ Jangan langsung buat payroll.

Buat dulu struktur dasar:

* `basic_salary`
* `allowance`
* `default_deduction`

---

# ⏱️ PHASE 4 – Attendance System (Week 6)

---

## ✅ Step 11 – Check In API

* Cegah double check-in
* Simpan latitude & longitude

---

## ✅ Step 12 – Check Out API

* Validasi sudah check-in
* Hitung total jam kerja

---

## ✅ Step 13 – Attendance Report

Fitur:

* Filter by date
* Filter by employee
* Export CSV

### Skill yang dilatih:

* Query optimization
* Indexing

---

# 🌴 PHASE 5 – Leave Workflow (Week 7–8)

---

## ✅ Step 14 – Leave Request

* Status default: `pending`
* Hitung total hari otomatis

---

## ✅ Step 15 – Approval Flow

Alur approval:

1. Manager approve
2. HR final approve
3. Kurangi quota cuti

---

## ✅ Step 16 – Prevent Overlapping Leave

⚠️ Bagian ini tricky.

Tidak boleh:

* Cuti di tanggal yang sama
* Melebihi quota cuti

---

# 💰 PHASE 6 – Payroll System (Week 9–10)

> 🔥 Ini bagian paling sulit.

---

## ✅ Step 17 – Payroll Period

* Buat periode payroll
* Lock period setelah final

---

## ✅ Step 18 – Generate Payroll (Service Layer)

Buat `PayrollService`:

```bash
PayrollService
 ├── calculateBasicSalary()
 ├── calculateAllowance()
 ├── calculateDeduction()
 ├── calculateTax()
```

### Wajib gunakan:

* DB Transaction
* Jangan simpan hasil perhitungan secara realtime

---

## ✅ Step 19 – Payroll Lock

Jika:

```bash
is_locked = true
```

➡️ Payroll tidak bisa diubah lagi.

---

# 📊 PHASE 7 – Performance Review (Week 11)

---

## ✅ Step 20 – Review System

* Manager input score
* HR melihat report

---

# 🔒 PHASE 8 – Hardening & Enterprise Layer (Week 12)

---

## ✅ Step 21 – Audit Log

Catat semua aktivitas:

* Create
* Update
* Delete

---

## ✅ Step 22 – Notification System

* Email notification
* In-app notification

---

## ✅ Step 23 – Queue System

Digunakan untuk:

* Payroll generation
* Email sending

---

## ✅ Step 24 – Testing

Wajib ada:

* Feature test
* Unit test
* API test

---

# 🎯 Final Goal

Jika kamu menyelesaikan semua phase ini:

* Kamu sudah berada di level **Enterprise Backend Developer**
* Kamu memahami:

  * Clean Architecture
  * Service Layer Pattern
  * Transaction Handling
  * RBAC
  * Workflow System
  * Payroll Calculation Logic

---

Kalau kamu mau, saya bisa bantu ubah ini jadi **versi roadmap belajar pribadi kamu** lengkap dengan checklist mingguan supaya bisa kamu pakai sebagai tracking progress 🚀
