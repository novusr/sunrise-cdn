# Sunrise SA-MP Mobile — CDN & Game Cache Hosting

Repositori ini berfungsi sebagai server CDN publik untuk distribusi resource dan manifest file game **Sunrise SA-MP Mobile**.

---

## 📡 Endpoint URLs

### 1. Manifest Files (Raw GitHub CDN)
| File | URL |
|---|---|
| **update.json** | `https://raw.githubusercontent.com/novusr/sunrise-cdn/main/update.json` |
| **data.json** | `https://raw.githubusercontent.com/novusr/sunrise-cdn/main/data.json` |
| **servers.json** | `https://raw.githubusercontent.com/novusr/sunrise-cdn/main/servers.json` |
| **changelog.txt** | `https://raw.githubusercontent.com/novusr/sunrise-cdn/main/changelog.txt` |
| **faq.json** | `https://raw.githubusercontent.com/novusr/sunrise-cdn/main/faq.json` |

---

## 📦 Game Cache Storage Architecture

File game cache didistribusikan melalui kombinasi dua layer CDN:

1. **GitHub Raw CDN (`main/files/...`)**  
   Untuk 277 file standar (< 50 MB, total ~274 MB) seperti audio, anim, textures ringan, scriptfiles, data files.
   ```
   https://raw.githubusercontent.com/novusr/sunrise-cdn/main/files/<relative_path>
   ```

2. **GitHub Releases CDN (`releases/download/...`)**  
   Untuk file besar (> 100 MB) yang melampaui batasan commit GitHub (mendukung resume download & tanpa batas 100 MB):
   - `texdb/gta3.img` (271 MB)
   - `texdb/gta3/gta3.etc.dat` (177 MB)
   - `com.rxdjv.sampmobile.7z` (272 MB archive)

Semua URL file ini telah dipetakan otomatis ke dalam `data.json` lengkap beserta ukuran file (*bytes*) dan checksum (*MD5*) untuk verifikasi integritas oleh PRDownloader di launcher Android.

---

## 🔧 Konfigurasi di Android Launcher (`Utils.java`)

Untuk menghubungkan aplikasi client launcher ke CDN ini, perbarui konfigurasi `web` pada `app/src/main/java/com/rxdjv/sampmobile/launcher/utils/Utils.java`:

```java
public static final String web = "https://raw.githubusercontent.com/novusr/sunrise-cdn/main/";
public static final String update = web + "update.json";
public static final String discord = web + "discord";
public static final String changelog = web + "changelog.txt";
public static final String hostedServersFileStr = web + "servers.json";
```
