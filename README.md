
# MikroTik Script: Telegram Bot

_Script_ ini digunakan untuk mengontrol MikroTik Anda hanya dengan menggunakan sosial media Telegram. Terdapat banyak perintah untuk memantau, mengubah _hotspot_, menghapus _user hotspot_, menambahkan akun _hotspot_ baru, mengubah _password user hotspot_, dan lain-lain.

# Daftar Isi
- [Disclaimer](#disclaimer)
- [Riwayat Versi](#riwayat-versi)
- [Instalasi](#instalasi)
- [Perintah-Perintah, Parameter, dan Fungsinya](#perintah-perintah-parameter-dan-fungsinya)
- [Sumber](#sumber)

# Disclaimer
_Script_ ini bersifat _open-source_. Anda dapat memodifikasi, menambah, ataupun mengurangi isi dari _script_ ini selama tidak melanggar ketentuan yang berlaku dalam lisensi _MIT_. _Script_ ini **TIDAK ADA GARANSI** selama Anda menggunakannya.

# Kontribusi
Kontribusi pada _repository_ ini hanya terbatas pada MikroTik Script dan Dokumentasi saja. Anda dapat berkontribusi dengan cara _Fork repository ini_, membuat _branch_ baru, lakukan perubahan, dan lakukan _Pull Request_ ke _repository_ ini. Deskripsikan apa saja yang Anda tambahkan dan apa yang Anda ubah di dalam _repository_ ini.

# Riwayat Versi
#### 1.2 (11 Agustus 2019)
 1. Perbaikan _bug_ saat _import script_ (error ``invalid default argument``)
 2. Pembaruan perintah pada hotspot:
   - Mengganti perintah ``/hotspot users`` menjadi ``/hotspot session count``
   - Mengganti perintah ``/hotspot showall`` menjadi ``/hotspot session showall``
   - Menambah perintah baru: ``/hotspot session deauth-by-mac``, ``/hotspot session deauth-by-ip``, dan ``/hotspot session deauth-by-user``
 3. Perbaikan perintah:
   - ``/reboot`` kini dapat digunakan untuk menghidupkan ulang _router_ (_delay_ 30 detik)
 4. Penambahan kondisi baru:
   - Setelah _reboot_, _Router_ akan mengirimkan laporan via Telegram bahwa dirinya telah melakukan _reboot_ dan mencatat semua kasus mengapa ia melakukan itu ke dalam "Critical Log" (jeda 30 detik setelah router selesai _reboot_).

#### 1.1 (8 Agustus 2019)
 1. Versi pertama

## Instalasi
Sebelum mulai instalasi, Anda harus memiliki _Access Token_ untuk Bot Telegram dan ChatID nya. Ikuti [link ini (labkom.co.id)](https://labkom.co.id/mikrotik/mikrotik-netwach-monitoring-status-access-point-hotspot-dengan-menggunakan-telegram) untuk paduan cara membuat bot telegram
Untuk cara menginstalnya, silahkan _clone_ atau _download repository_ ini, lalu:

 1. Ekstrak file ZIP yang sudah Anda _download_ (lewati jika anda _clone repository_ ini)
 2. _Upload_ file ``telegram_bot.rsc`` ke dalam MikroTik Anda (bisa lewat FileZilla FTP, bisa juga lewat WinBox) dan simpan ke folder utama (root atau /) di MikroTik Anda.
 3. Setelah itu, buka _Terminal_ MikroTik dan ketikkan perintah berikut:
 ``import file-name=telegram_bot.rsc``
 4. Konfigurasikan pengaturan _bot_ nya di ``System > Scripts > tg_config`` dengan mengubah perintah berikut:
 > Isi dengan Access Token Bot Telegram Anda:
   ``"botAPI"="xxxxxx:xxxxxxxx-xxxxxxx"`` 

 > Isi dengan Access Token Bot Telegram Anda:
    ``defaultChatID"="xxxxxxxxxx"``
    
> Isi dengan beberapa ChatID Anda, bisa personal, bisa grup. Pisahkan dengan tanda koma:
  ``"trusted"="xxxxxxxxxx, xxxxxxxxx, -xxxxxxxxx"``
  
  Lalu simpan konfigurasinya.
  
  5. Selesai!

## Perintah-Perintah, Parameter, dan Fungsinya
Ketikkan perintah berikut pada kolom _chatting_ Anda dengan _bot_ Telegram Anda. Setiap _parameter_ yang dimasukkan, dipisahkan dengan menggunakan spasi, misalnya ``/interface show``.

| Perintah | Parameter | Fungsi | Contoh |
|-----------|--------------|-------|-----|
| ``/help`` | | Menampilkan daftar fungsi yang dapat dieksekusi | |
| ``/start`` | | Menampilkan daftar fungsi yang dapat dieksekusi | |
| ``/cpu`` | | Menampilkan Router ID, Load CPU, Uptime, dan total RAM yang terpakai | |
| ``/dhcp`` | ``lease`` | menampilkan seluruh detail pada DHCP Lease| ``/dhcp lease`` |
| ``/interface`` | ``show`` | Menampilkan status terhubungnya antar port Ethernet di MikroTik | ``/interface show`` |
| ``/interface`` | ``show all`` | Menampilkan status terhubungnya seluruh interface di MikroTik | ``/interface show all`` |
| ``/hotspot`` | ``session count`` | Menampilkan jumlah user yang sedang aktif | ``/hotspot session count`` |
| ``/hotspot`` | ``session showall`` | Menampilkan seluruh detail user yang sedang aktif mulai dari Username sampai Uptime (kecuali password) | ``/hotspot session showall`` |
| ``/hotspot`` | ``session deauth-by-user <username>`` | Mencabut _session_ perangkat berdasarkan Username | ``/hotspot session deauth-by-user telecomadmin`` |
| ``/hotspot`` | ``session deauth-by-ip <ip>`` | Mencabut _session_ perangkat berdasarkan Alamat IP | ``/hotspot session deauth-by-ip 192.168.1.2`` |
| ``/hotspot`` | ``session deauth-by-mac <mac address>`` | Mencabut _session_ perangkat berdasarkan Alamat MAC | ``/hotspot session deauth-by-mac AB:CD:EF:01:23:45`` |
| ``/hotspot`` | ``add <username> <password>`` | Menambahkan user hotspot baru | ``/hotspot add telecomadmin admintelecom`` |
| ``/hotspot`` | ``delete <username>`` | Menghapus user hotspot secara permanen | ``/hotspot delete telecomadmin`` |
| ``/hotspot`` | ``disable <username>`` | Mematikan atau menonaktifkan user hotspot | ``/hotspot disable telecomadmin`` |
| ``/hotspot`` | ``enable <username>`` | Mengaktifkan user hotspot yang dinonaktifkan | ``/hotspot enable telecomadmin`` |
| ``/hotspot`` | ``change-password <username> <password baru>`` | Mengubah password user hotspot | ``/hotspot change-password telecomadmin p4ssw0rdny4`` |
| ``/ping`` | | Melakukan ping ke DNS Google | ``/ping`` |
| ``/ping`` | ``to <ip address>`` | Melakukan ping ke alamat IP tertentu | ``/ping to 127.0.0.1`` |
| ``/public`` | | Menampilkan Dynamic DNS dan Public IP pada MikroTik Anda | ``/public`` |
| ``/enablehotspot`` | | Mengaktifkan seluruh fungsi hotspot | ``/enablehotspot`` |
| ``/disablehotspot`` | | Menonaktifkan seluruh fungsi hotspot | ``/disablehotspot`` |
| ``/forceupdateddns`` | | Memperbarui Dynamic DNS secara paksa | ``/forceupdateddns`` |
| ``/reboot`` | | Menghidupkan ulang MikroTik (jeda 30 detik sebelum menghidupkan ulang) | ``/reboot`` |

> **Catatan**: untuk dapat menjalankan perintah ``/disablehotspot``,  ``/enablehotspot``, dan ``/interface show``, silakan Anda konfigurasikan sendiri hotspot mana yang akan di "otomatis" kan di script ``tg_cmd_disablehotspot``, ``tg_cmd_enablehotspot``, dan ethernet mana saja yang akan ditampilkan di ``tg_cmd_interface``.

# Sumber

 - [Labkom](https://labkom.co.id)
 - [Forum MikroTik (EN)](https://forum.mikrotik.com)
 - [Telegram API (EN)](https://api.telegram.org)


