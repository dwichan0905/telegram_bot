# MikroTik Script: Telegram Bot

_Script_ ini digunakan untuk mengontrol MikroTik Anda hanya dengan menggunakan sosial media Telegram. Terdapat banyak perintah untuk memantau, mengubah _hotspot_, menghapus _user hotspot_, menambahkan akun _hotspot_ baru, mengubah _password user hotspot_, dan lain-lain.

# Disclaimer
_Script_ ini bersifat _open-source_. Anda dapat memodifikasi, menambah, ataupun mengurangi isi dari _script_ ini selama tidak melanggar ketentuan yang berlaku dalam lisensi _MIT_. _Script_ ini **TIDAK ADA GARANSI** selama Anda menggunakannya.

## Instalasi
Sebelum mulai instalasi, Anda harus memiliki _Access Token_ untuk Bot Telegram dan ChatID nya. Ikuti [link ini (labkom.co.id)](https://labkom.co.id/mikrotik/mikrotik-netwach-monitoring-status-access-point-hotspot-dengan-menggunakan-telegram) untuk paduan cara membuat bot telegram
Untuk cara menginstalnya, silahkan _clone_ atau _download repository_ ini, lalu:

 1. Ekstrak file ZIP yang sudah Anda _download_ (lewati jika anda _clone repository_ ini)
 2. _Upload_ file ``telegram_bot.rsc`` ke dalam MikroTik Anda (bisa lewat FileZilla FTP, bisa juga lewat WinBox) dan simpan ke folder utama (root atau /) di MikroTik Anda.
 3. Setelah itu, buka _Terminal_ MikroTik dan ketikkan perintah berikut:
 ``import file-name=telegram_bot.rsc``
 4. Konfigurasikan pengaturan _bot_ nya di ``System > Scripts > tg_config`` dengan mengubah perintah berikut:
 
   ``"botAPI"="xxxxxx:xxxxxxxx-xxxxxxx"; #isi dengan Access Token Bot Telegram Anda``
   
  ``defaultChatID"="xxxxxxxxxx"; #isi dengan ChatID Anda``
  
  ``"trusted"="xxxxxxxxxx, xxxxxxxxx, -xxxxxxxxx"; #isi dengan beberapa ChatID Anda, bisa personal, bisa grup. Pisahkan dengan tanda koma ``
  Lalu simpan komfigurasinya.
  5. Selesai!

## Perintah-Perintah, Parameter, dan Fungsinya
Setiap parameter yang dimasukkan, dipisahkan dengan menggunakan spasi. misalnya ``/interface show``.

| Perintah | Parameter | Fungsi | Contoh |
|-----------|--------------|-------|-----|
| ``/help`` | | Menampilkan daftar fungsi yang dapat dieksekusi | |
| ``/start`` | | Menampilkan daftar fungsi yang dapat dieksekusi | |
| ``/cpu`` | | Menampilkan Router ID, Load CPU, Uptime, dan total RAM yang terpakai | |
| ``/interface`` | ``show`` | Menampilkan status terhubungnya antar port Ethernet di MikroTik | |
| ``/hotspot`` | ``users`` | Menampilkan jumlah user yang sedang aktif | ``/hotspot users`` |
| ``/hotspot`` | ``showall`` | Menampilkan seluruh detail user yang sedang aktif mulai dari Username sampai Uptime (kecuali password) | ``/hotspot showall`` |
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
| ``/reboot`` | | Menghidupkan ulang MikroTik | ``/reboot`` |

> **Catatan**: untuk dapat menjalankan perintah ``/disablehotspot``
dan ``/enablehotspot``, silakan Anda konfigurasikan sendiri hotspot mana yang akan di "otomatis" kan di script ``tg_cmd_disablehotspot`` dan di ``tg_cmd_enablehotspot``.

# Sumber

 - labkom.co.id
 - forum.mikrotik.com
 - api.telegram.org

