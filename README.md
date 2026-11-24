# E-Arsip SDN 101731 (GitHub Pages + Google Sheets + Apps Script)

Aplikasi pencatatan nomor surat. Tampilan di GitHub Pages, data di Google Sheets, dihubungkan lewat Google Apps Script.

```
Browser (GitHub Pages: index.html)  ⇄  Apps Script Web App (Code.gs)  ⇄  Google Sheets
```

## 1. Siapkan database & backend

1. Buat Google Sheets baru, beri nama mis. **E-Arsip SDN 101731**.
2. Menu **Ekstensi → Apps Script**. Hapus isi default, tempel seluruh isi `Code.gs`.
3. Ubah baris `const APP_PIN = 'ganti-pin-ini';` menjadi PIN rahasia Anda.
4. Klik **Terapkan (Deploy) → Deployment baru → Jenis: Aplikasi web**
   - Jalankan sebagai: **Saya**
   - Siapa yang memiliki akses: **Siapa saja**
5. Setujui izin akses, lalu **salin URL Web App** (berakhiran `/exec`).

Sheet `Arsip` dan `Klasifikasi` dibuat otomatis pada akses pertama.

> Setiap kali `Code.gs` diubah, lakukan **Terapkan → Kelola deployment → Edit → Versi baru → Terapkan**. URL tetap sama.

## 2. Pasang di GitHub Pages

1. Buat repository baru di GitHub, upload `index.html` (dan `README.md` bila mau). **Jangan upload `Code.gs` berisi PIN ke repo publik** — cukup simpan di Apps Script.
2. **Settings → Pages → Branch: main / root → Save**.
3. Buka `https://<username>.github.io/<nama-repo>/`.
4. Isi **URL Web App** dan **PIN**, lalu Hubungkan. Tersimpan di browser tiap perangkat.

Opsional: isi `DEFAULT_API_URL` di `index.html` agar URL tidak perlu diketik di tiap perangkat (PIN tetap diketik).

## 3. Memindahkan data lama

1. Di **aplikasi lama**, klik ikon **Download** (Export Semua Data) → dapat file `arsip_lengkap_seluruh_tahun.csv`.
2. Di **aplikasi baru**, klik ikon **Upload** → pilih file CSV tadi → cek pratinjau → **Import**.

Import melewati nomor surat yang sudah ada (anti-duplikat), jadi aman diulang. Format CSV export baru sama persis dengan yang lama, jadi bisa dipakai bolak-balik. Tanggal format `dd/mm/yyyy` juga dikenali.

## Catatan

- **Backup**: Google Sheets Anda adalah databasenya. Gunakan *File → Download* atau *Riwayat versi*.
- **Keamanan**: halaman web publik, tetapi data hanya bisa dibaca/ditulis dengan PIN yang benar. Gunakan PIN yang tidak mudah ditebak.
- **Nomor urut ganda**: server menolak simpan jika nomor lengkap sudah ada.
- Edit langsung di Sheets boleh dilakukan; baris tanpa `id` otomatis diberi id saat aplikasi memuat data. Jangan mengubah nama sheet/header.
