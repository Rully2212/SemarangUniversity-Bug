# Write-up: IDOR on E-Learning Student Profiles

## Description
Celah **Insecure Direct Object Reference (IDOR)** ditemukan pada platform E-Learning Moodle USM. Sistem tidak memvalidasi kepemilikan data saat seorang pengguna mengakses profil pengguna lain melalui manipulasi parameter ID.

## Proof of Concept (PoC)
1. Login dengan akun mahasiswa resmi.
2. Akses profil pribadi di URL: `https://elearning.usm.ac.id/user/profile.php?id=38480`.
3. Mengubah ID menjadi `38475`.
4. Sistem menampilkan profil lengkap mahasiswa lain, termasuk:
   - Nama Lengkap
   - Alamat Email Student
   - Lokasi (Kota)
   - Daftar Kursus yang diikuti.

## Impact
- **Privacy Breach:** Kebocoran data pribadi mahasiswa (PII).
- **Mass Harvesting:** Penyerang dapat mengumpulkan ribuan email aktif mahasiswa USM untuk target serangan phishing.

## Recommendation
Implementasikan pemeriksaan otorisasi di sisi server (Server-side Access Control) untuk memastikan user hanya bisa melihat profil yang diizinkan.
