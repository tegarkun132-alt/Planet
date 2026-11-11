# Panduan Memasukkan Media Pembelajaran ke Adobe Animate (HTML5 Canvas)

Paket ini berisi seluruh **codingan JavaScript (CreateJS)**, **aset vektor SVG planet & background**, serta **preview web interaktif** (`preview-web/index.html`) untuk media pembelajaran IPA **Jelajah Tata Surya**.

---

## 1. Buat Dokumen Baru di Adobe Animate
1. Buka Adobe Animate -> pilih **`File > New`** (`Ctrl + N`).
2. Pilih tab **Education** atau **Web**, lalu pilih tipe dokumen **`HTML5 Canvas`**.
3. Atur ukuran panggung (**Properties**):
   - **Width**: `1280` px
   - **Height**: `720` px
   - **FPS**: `30`
4. Import seluruh file `.svg` dari folder `assets/svg/` lewat **`File > Import > Import to Library...`**.

---

## 2. Siapkan 4 Layer & 7 Frame di Timeline Utama
Buat **4 Layer** dari atas ke bawah seperti ini:

| Urutan | Nama Layer | Fungsi | Frame 1..7 |
| :--- | :--- | :--- | :--- |
| 1 | `Actions` | Tempat codingan JS per frame | **7 Blank Keyframe (`F7`)** di frame 1–7 |
| 2 | `Labels` | Nama label setiap halaman | **7 Blank Keyframe (`F7`)** di frame 1–7 |
| 3 | `Konten` | Tombol, teks dinamis, planet, pop-up | **7 Blank Keyframe (`F7`)** di frame 1–7 |
| 4 | `Background` | Gambar latar luar angkasa (`bg-luar-angkasa.svg`) | Keyframe di Frame 1, tekan **`F5`** di Frame 7 |

### Isi Frame Label (Layer `Labels`)
Klik masing-masing keyframe di layer **`Labels`**, lalu buka **Properties > Label > Name** dan isi persis seperti tabel berikut (huruf kecil semua, tanpa spasi):

| Frame | Frame Label | File Script (`animate-scripts/`) |
| :---: | :--- | :--- |
| **1** | `beranda` | `01-frame-beranda.js` |
| **2** | `menu` | `02-frame-menu.js` |
| **3** | `materi` | `03-frame-materi.js` |
| **4** | `eksplorasi` | `04-frame-eksplorasi.js` |
| **5** | `game` | `05-frame-game-dragdrop.js` |
| **6** | `kuis` | `06-frame-kuis.js` |
| **7** | `hasil` | `07-frame-hasil.js` |

---

## 3. Daftar Instance Name Wajib di Setiap Frame (Layer `Konten`)

> **Penting:** Untuk mengatur **Instance Name**, klik objek di Stage -> buka panel **Properties** -> isi kotak `<Instance Name>`. Huruf besar-kecil harus sama persis!

### Frame 1 (`beranda`)
- `btnMulai` *(Button atau MovieClip)* — tombol "Mulai Belajar".

### Frame 2 (`menu`)
- `btnMenuMateri` *(Button/MovieClip)* — menuju halaman Materi.
- `btnMenuEksplorasi` *(Button/MovieClip)* — menuju Eksplorasi Planet (Pop-up).
- `btnMenuGame` *(Button/MovieClip)* — menuju Mini Game Drag & Drop.
- `btnMenuKuis` *(Button/MovieClip)* — menuju Kuis Pilihan Ganda.
- `btnKembaliBeranda` *(Opsional)* — kembali ke Beranda.

### Frame 3 (`materi`)
- `txtJudulMateri` *(Dynamic Text)*
- `txtSubjudulMateri` *(Dynamic Text — opsional)*
- `txtIsiMateri` *(Dynamic Text — ubah **Behavior** menjadi `Multiline`)*
- `txtHalaman` *(Dynamic Text)*
- `mcGambarMateri` *(MovieClip opsional berisi 5 frame ilustrasi untuk masing-masing slide)*
- `btnPrev` *(Button/MovieClip)*
- `btnNext` *(Button/MovieClip)*
- `btnHome` *(Button/MovieClip)*

### Frame 4 (`eksplorasi`) — Pop-up Interaktif
- **9 Objek Planet** *(ubah masing-masing SVG planet menjadi **MovieClip**)*:
  `obj_matahari`, `obj_merkurius`, `obj_venus`, `obj_bumi`, `obj_mars`, `obj_jupiter`, `obj_saturnus`, `obj_uranus`, `obj_neptunus`
- `popupBackdrop` *(Opsional: MovieClip kotak hitam `1280x720` opacity 60% tepat di bawah `popupInfo`)*
- `popupInfo` *(MovieClip panel pop-up — taruh paling atas di frame 4)*. **Klik 2x ke dalam `popupInfo`** lalu buat komponen berikut:
  - `txtNama` *(Dynamic Text)*
  - `txtKategori` *(Dynamic Text)*
  - `txtInfoSingkat` *(Dynamic Text)*
  - `txtDeskripsi` *(Dynamic Text, Behavior: `Multiline`)*
  - `mcIkonPopup` *(MovieClip opsional berisi 9 frame ikon planet berurutan dari Matahari s/d Neptunus)*
  - `btnTutupPopup` *(Button/MovieClip tombol `X` / Tutup)*
- `btnHome` *(Button/MovieClip)*

### Frame 5 (`game`) — Mini Game Drag & Drop
- `txtJudulRonde` *(Dynamic Text)*
- `txtSkorGame` *(Dynamic Text)*
- `txtFeedbackGame` *(Dynamic Text)*
- **4 Kartu yang digeser** *(WAJIB **MovieClip**, bukan Button)*:
  `drag_1`, `drag_2`, `drag_3`, `drag_4`
  *(Klik 2x ke dalam masing-masing `drag_X`, buat kotak kartu + 1 Dynamic Text bernama `txtLabel`)*
- **4 Kotak Target Jatuh** *(WAJIB **MovieClip**)*:
  `drop_1`, `drop_2`, `drop_3`, `drop_4`
  *(Klik 2x ke dalam masing-masing `drop_X`, buat kotak target dengan isi/fill semi-transparan agar mudah disentuh + 1 Dynamic Text `Multiline` bernama `txtLabel`)*
  > Catatan: `drag_1` berpasangan dengan `drop_1`, `drag_2` dengan `drop_2`, dst. **Jangan khawatir soal urutan lurus**, karena kode otomatis mengacak posisi awal `drag_1..4` setiap kali ronde dimulai!
- `btnResetGame` *(Button/MovieClip)*
- `btnGantiRonde` *(Button/MovieClip — opsional, pindah Ronde 1 <-> Ronde 2)*
- `btnHome` *(Button/MovieClip)*

### Frame 6 (`kuis`) — Kuis Pilihan Ganda
- `txtNomorSoal` *(Dynamic Text)*
- `txtSkorSementara` *(Dynamic Text)*
- `txtSoal` *(Dynamic Text, Behavior: `Multiline`)*
- `txtPembahasan` *(Dynamic Text, Behavior: `Multiline` — opsional)*
- **4 Tombol Pilihan Jawaban** *(WAJIB **MovieClip**, bukan Button)*:
  `btnOpsiA`, `btnOpsiB`, `btnOpsiC`, `btnOpsiD`
  - Klik 2x ke dalam setiap `btnOpsiX`, buat latar tombol + 1 Dynamic Text `Multiline` bernama `txtLabel`.
  - *(Opsional keren)* Di dalam timeline `btnOpsiX`, buat 3 frame berlabel **`normal`** (frame 1), **`benar`** (frame 2 - warna hijau), dan **`salah`** (frame 3 - warna merah), plus `this.stop();` di frame 1-nya. Kode otomatis mengganti warna tombol saat siswa menjawab!
- `btnLanjutSoal` *(MovieClip berisi Dynamic Text `txtLabel` — tombol "Soal Berikutnya" / "Lihat Hasil"; jika pakai `Button`, letakkan Dynamic Text `txtBtnLanjut` di atas tombolnya)*
- `btnHome` *(Button/MovieClip)*

### Frame 7 (`hasil`)
- `txtSkorAkhir` *(Dynamic Text, font besar untuk angka 0–100)*
- `txtJumlahBenar` *(Dynamic Text)*
- `txtPredikat` *(Dynamic Text, Behavior: `Multiline`)*
- `btnUlangiKuis` *(Button/MovieClip)*
- `btnHome` *(Button/MovieClip)*

---

## 4. Memasang Codingan ke Panel Actions (`F9`)

1. Buka panel Actions (**Window > Actions** atau tekan **`F9`**).
2. Di sidebar kiri panel Actions, klik **`Global > Script`**, lalu paste seluruh isi file **`00-global-data-dan-helper.js`**.
   *(Alternatif jika tidak ketemu `Global > Script`: paste isi `00-global-data-dan-helper.js` di baris paling atas **Frame 1**).*
3. Klik masing-masing keyframe pada layer **`Actions`** dari Frame 1 sampai Frame 7, lalu paste isi file `01-frame-beranda.js` sampai `07-frame-hasil.js` sesuai nomor framenya.

---

## 5. Pengaturan Publish & Tips Anti-Error

1. **Responsive agar pas di Laptop & HP**:
   Buka **Publish Settings** (`Ctrl + Shift + F12`) -> centang **Center stage** (`Both`) dan centang **Make responsive** (`Both`, pilih `Fit in view`).
2. **Jangan pakai `Button` symbol untuk tombol yang teksnya berubah dinamis** (`btnOpsiA..D`, `drag_1..4`, `drop_1..4`, `btnLanjutSoal`). Gunakan **`MovieClip`**, karena pada HTML5 Canvas teks dinamis di dalam symbol `Button` tidak bisa diubah stabil lewat kode.
3. **Ingin menambah efek suara (opsional)?**
   Import file `.mp3`/`.wav` ke **Library**, klik ganda kolom **Linkage** di Library dan beri nama persis:
   - `sfx_klik`
   - `sfx_benar`
   - `sfx_salah`
   Kode sudah otomatis memutar suara tersebut jika tersedia!
4. **Mengedit / Mengganti Materi & Soal**:
   Semua teks materi, data 9 planet, pasangan drag-drop, dan 10 soal kuis tersimpan rapi di satu tempat yaitu objek `MTS.DATA` di file **`00-global-data-dan-helper.js`**.
5. **Uji Coba**: Tekan **`Ctrl + Enter`** untuk langsung menjalankan media pembelajaran di browser!
