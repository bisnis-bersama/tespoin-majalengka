MIGRASI FIREBASE - TESPOIN MAJALENGKA

Perubahan yang dilakukan pada paket ini:
- index.html membaca pengaturan/acara dari Firestore, tidak lagi memanggil Google Apps Script.
- lunas.html membaca koleksi peserta langsung dari Firestore.
- Registrasi mempertahankan OCR di browser dan hanya menyimpan teks OCR/nama file ke Firestore; file bukti tidak diunggah.
- Harga registrasi mengikuti tier aktif berdasarkan tanggal pada pengaturan/acara; tidak memakai harga tetap Rp150.000 sebagai harga final.
- Registrasi membuat dokumen peserta dan reservasi uniqueWa/uniqueEmail secara batch agar halaman publik tidak perlu membaca seluruh koleksi peserta.
- Halaman scan memakai nama field jamCheckIn, waktuScan, dan petugasScan yang sesuai dengan aturan keamanan.
- Tautan pengalihan login staff disesuaikan ke login-panitia.html.
- Ditambahkan halaman registrasi-cod.html dan register-cod.html berbasis Firestore.

PENTING SEBELUM DIPAKAI:
1. Periksa file firestore.rules dan storage.rules, lalu terapkan melalui Firebase Console hanya setelah membandingkannya dengan rules aktif proyek. Jangan menghapus koleksi/data.
2. Pengaturan publik memerlukan izin read pada dokumen pengaturan/acara.
3. Registrasi publik memerlukan Firebase Authentication Anonymous diaktifkan.
4. Registrasi membuat uniqueWa dan, jika email diisi, uniqueEmail. Aturan create-only mencegah key baru yang sama dipakai ulang. Data peserta lama perlu dibuatkan dokumen reservasi unik oleh admin; jangan menghapus peserta lama.
5. Halaman COD hanya untuk admin/owner, dan hanya aktif pada tanggal acara jika codHarga sudah diatur. Aturan Firestore harus mengizinkan create COD staff seperti pada file rules ini.
6. Halaman pengaturan mengunggah gambar ke Firebase Storage pada folder slides/. Periksa storage.rules sebelum mengunggah.
7. ZIP ini belum dapat diuji terhadap Firebase live dari lingkungan ini. Uji di project/staging terlebih dahulu: registrasi, duplikasi, tier, pengaturan, verifikasi lunas, COD, dashboard, bukti, dan check-in. Jangan menganggap deploy berhasil sebelum tes tersebut lolos.


KOREKSI HAK AKSES (9 OKTOBER 2026)
- Admin: seluruh fungsi termasuk edit, hapus, approval, pengaturan, dan check-in.
- Owner: fungsi operasional termasuk pengaturan dan check-in; tidak boleh edit, hapus, atau approval.
- Peserta: hanya halaman publik index.html dan registrasi.html.
- Firestore Rules sudah disesuaikan agar check-in dapat dilakukan Admin maupun Owner.
- Jangan mengganti Rules aktif sebelum memeriksa kebutuhan aplikasi dan menguji di Firebase.
