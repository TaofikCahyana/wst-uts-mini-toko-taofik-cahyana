# Laporan UTS Web Software Tools
**Nama: TAOFIK CAHYANA**
**Nomor Induk Mahasiswa: 12523029**
**Kelas: B**
**Tanggal: 13-11-2026**

## A. Bukti pemeriksaan masalah
| Masalah | Alat yang digunakan | Bukti pemeriksaan | Perkiraan penyebab | Perbaikan | Hasil setelah perbaikan |
| --- | --- | --- | --- | --- | --- |
1. Masalah Produk (Gagal Memuat Katalog)
- Alat yang digunakan: Browser Developer Tools (Network tab, Console).
- Bukti pemeriksaan: Muncul error status 404 Not Found pada rute /api/barang ketika halaman mencoba memuat data produk.
- Perkiraan penyebab: Ketidakcocokan penamaan endpoint API di sisi backend server (/api/products) dengan rute yang dipanggil pada file app.js (/api/barang).
- Perbaikan: Mengubah rute fetch pada file public/app.js dari /api/barang menjadi /api/products.
- Hasil setelah perbaikan: Produk berhasil dimuat dari server dan tampil di katalog browser dengan keterangan "4 produk tersedia".

2. Masalah Tombol Keranjang (Tidak Merespons)
- Alat yang digunakan: Browser Elements tab, Console.
- Bukti pemeriksaan: Tombol "+ Tambah ke Keranjang" tidak merespons ketika diklik dan event listener gagal terikat ke tombol.
- Perkiraan penyebab: Ketidaksesuaian selektor kelas elemen tombol di dalam file app.js (.add-to-cart) dengan kelas HTML yang sebenarnya tertulis pada template (.add-button).
- Perbaikan: Mengubah selektor query di public/app.js dari .add-to-cart menjadi .add-button.
- Hasil setelah perbaikan: Tombol berhasil merespons klik dengan baik, dan produk otomatis masuk serta bertambah ke dalam panel keranjang.

3. Masalah Total Belanja (Perhitungan Harga)
- Alat yang digunakan: Unit Testing (node --test), Browser UI.
- Bukti pemeriksaan: Total harga di keranjang hanya menghitung harga satuan mentah (item.price) tanpa memperhitungkan jumlah kuantitas barang yang dibeli.
- Perkiraan penyebab: Rumus di dalam fungsi calculateTotal pada file src/cart.js hanya menjumlahkan harga satuan tanpa faktor pengali kuantitas.
- Perbaikan: Memperbarui rumus di src/cart.js menjadi total + (item.price * item.quantity).
- Hasil setelah perbaikan: Total belanja di keranjang terhitung akurat sesuai jumlah kuantitas barang dan lulus seluruh unit test otomatis (pass 7).

## B. Hasil pengujian
* Jumlah pengujian sebelum perbaikan: 7 unit test (gagal / belum akurat pada perhitungan kuantitas & fungsionalitas tombol tidak aktif).
* Jumlah pengujian berhasil setelah perbaikan: 7 unit test sukses (`pass 7`, `fail 0`).
* Catatan perubahan pada fungsi yang diperiksa:
1. Penyesuaian endpoint API produk dari `/api/barang` ke `/api/products`.
2. Perbaikan kelas event listener tombol dari `.add-to-cart` ke `.add-button`.
3. Perbaikan logika perhitungan total harga dengan mengikutsertakan kuantitas (`item.quantity`).



## C. Kualitas kode
* Temuan sebelum perbaikan: Terdapat *warning* variabel `discount` yang tidak terpakai di `src/cart.js` serta beberapa baris kode yang belum sesuai standar format otomatis Biome.
* Perbaikan yang dilakukan: Menghapus variabel `discount` yang tidak terpakai dan menjalankan perintah pemformatan otomatis (`npx @biomejs/biome format --write`).
* Hasil pemeriksaan ulang: Berhasil lolos pemeriksaan linter dan format (`npm run lint` & `format:check` bersih tanpa *warning* maupun *error*).

## D. Git
* Branch (jika membuat): `main` / `master`
* Ringkasan commit: `fix: selesaikan debugging UTS mini toko online dan lulus seluruh unit test`
* Hasil pemeriksaan `git status`: Seluruh file modifikasi (`public/app.js`, `src/cart.js`, `LAPORAN_UJIAN.MD`) telah siap dan tersimpan (*clean workspace*).

## E. Pemakaian kecerdasan buatan (jika digunakan)
* Nama alat: Gemini AI Collaborator
* Pertanyaan/instruksi yang diberikan: Membantu menganalisis error kode, mencari akar permasalahan pada file `app.js` dan `cart.js`, serta membimbing langkah-langkah pengujian lokal.
* Bagian jawaban yang diterapkan: Panduan perbaikan logika rute API, selektor tombol, rumus perkalian kuantitas keranjang, serta tata cara menjalankan perintah *testing* dan linter Biome.
* Cara memeriksa apakah saran tersebut benar: Menguji fungsionalitas secara langsung di browser lokal (`http://localhost:5057`), menjalankan pengujian otomatis dengan `node --test`, serta memverifikasi kualitas kode menggunakan `npm run lint`.

## F. Refleksi singkat
* Satu pelajaran paling penting dari ujian ini: Ketelitian dalam membaca pesan kesalahan (*error log* dan penelusuran *Developer Tools*) sangat penting untuk menemukan akar masalah dengan cepat, serta pentingnya menjaga kualitas kode (*code quality*) menggunakan alat bantu modern seperti Biome dan unit testing.
