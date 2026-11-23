# EF234302 Object-Oriented Programming — Quiz 2 (Profitina Laundry)

Repositori pengerjaan tugas kelompok Quiz 2 mata kuliah Pemrograman Berorientasi Objek (PBO / OOP). Proyek ini berfokus pada studi kasus sistem operasional laundry **Profitina Laundry** menggunakan implementasi ganda (Java dan Python) yang mencakup konsep *generic programming*, *collections*, *event-driven GUI/listeners*, serta pola arsitektur *View-Model*.

---

## Daftar Soal & Topik

| Kode Soal | Judul Soal | Topik Utama |
| :--- | :--- | :--- |
| **Q051** | *Orders per service: counting with a map* | Penghitungan frekuensi pesanan per jenis layanan menggunakan `Map` / dictionary. |
| **Q053** | *A generic bag for the sorting table* | Implementasi struktur data koleksi generik `Bag<T>` untuk meja pemilahan pakaian. |
| **Q054** | *Wildcards at the sorting desk* | Penerapan bounded wildcards (`<? extends T>` dan `<? super T>`) pada hierarki item laundry. |
| **Q060** | *Tracing the listeners of a quote panel* | GUI kalkulasi estimasi harga laundry berbasis event listener dan pembaruan komponen reaktif. |
| **Q075** | *A filtered, sorted order list: view-model* | Arsitektur View-Model untuk operasi *filtering* dan *sorting* daftar pesanan laundry menggunakan `Comparator`. |

---

## Panduan Kompilasi & Menjalankan Program

Setiap folder soal (`Q051` – `Q075`) memiliki subfolder `java/` dan `python/`. Jalankan perintah dari dalam direktori masing-masing soal.

### 1. Java

Buat folder output `classes` (jika belum ada), kompilasi file Java, lalu jalankan class utamanya:

```bash
# Contoh pada Q051:
cd Q051
mkdir classes
javac -d classes java/ServiceTally.java
java -cp classes ServiceTally
```

Daftar class utama untuk setiap soal:
- `Q051`: `ServiceTally`
- `Q053`: `BagDemo`
- `Q054`: `WildcardDesk`
- `Q060`: `QuotePanel` (bisa ditambahkan argumen `--selftest` jika tersedia)
- `Q075`: `OrderListViewModel`

### 2. Python

Jalankan skrip Python langsung menggunakan interpreter Python 3:

```bash
# Contoh pada Q051:
cd Q051
python python/service_tally.py
```

Daftar script untuk setiap soal:
- `Q051`: `python/service_tally.py`
- `Q053`: `python/bag_demo.py`
- `Q054`: `python/wildcard_desk.py`
- `Q060`: `python/quote_panel.py`
- `Q075`: `python/order_list_view_model.py`

---

## Aturan Kolaborasi Kelompok

1. Bekerja pada branch atau koordinasikan pengerjaan subfolder masing-masing anggota.
2. Jangan mengubah tanda tangan method (*method signatures*) atau kerangka kode bawaan soal di luar blok instruksi pengerjaan.
3. Jawab pertanyaan analisis teoritis di file `ANSWER.md` pada folder soal terkait (bila ada).
4. Pastikan file hasil kompilasi (`*.class`, `classes/`) dan cache Python tidak ter-commit ke repositori (sudah dikonfigurasi pada `.gitignore`).
