# Quick Start

## Untuk User: Download Langsung

1. Buka:
   `https://github.com/sintakaridina/delta-deploy/releases`
2. Download ZIP Windows terbaru.
3. Extract ZIP.
4. Double-click:
   `DeltaDeploy.exe`

App akan terbuka sebagai window desktop. Tidak perlu install Python dan tidak perlu membuka browser manual.

Saat window ditutup, server internal ikut berhenti.

## Alur Pakai Singkat

1. Klik `Add Connection`.
2. Isi data SSH server, lalu save.
3. Klik `Connect`.
4. Klik `Add Project` pada server yang sudah connected.
5. Isi local path dan remote path.
6. Isi exceptions jika ada.
7. Isi env-managed files jika ada, misalnya `.env` atau `config.yaml`.
8. Pilih project untuk membuka workspace deploy.
9. Klik `Refresh` untuk melihat file baru/modified/deleted.
10. Review file, lalu klik `Deploy Now`.

## Jalankan dari Source

```bash
pip install -r requirements.txt
python launcher.py
```

Mode ini juga membuka desktop window.

## Build `.exe` Windows

```bash
pip install -r requirements.txt
build.bat
```

Output:

```text
dist/DeltaDeploy.exe
```

Jika build gagal karena file terkunci, tutup app atau jalankan:

```powershell
Stop-Process -Name DeltaDeploy -Force
```

Lalu ulangi build.

## Buat ZIP untuk Dibagikan

```powershell
Compress-Archive -Path dist\DeltaDeploy.exe, README.md, QUICKSTART.md -DestinationPath DeltaDeploy-windows.zip -Force
```

Upload ZIP ke GitHub Releases supaya user bisa download langsung.

## Data Lokal

Storage:

```text
~/.delta-deploy/data.json
```

Folder backup lokal:

```text
backups/
```
