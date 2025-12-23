# ElStream (Linux Soundboard)

Konfigurasi **soundboard berbasis shortcut / keybind** di **Linux** yang berfungsi seperti **Stream Deck**, tanpa hardware tambahan.

Project ini memanfaatkan **keybind** untuk memutar suara (sound effect, voice clip, dll) menggunakan pemutar audio CLI. Cocok untuk:
- Soundboard streaming
- Shortcut efek suara
- Macro audio di Linux ringan

> ⚠️ **Bukan Elgato Stream Deck**  
> Ini adalah implementasi software-only menggunakan keyboard shortcut.

---

## 📂 Struktur Repository

```
.
├── .config/
│   └── openbox/
│       └── rc.xml        # Keybind Openbox
└── .streamdeck/          # File audio soundboard
```

---

## ⚙️ Prasyarat

Pastikan sudah terpasang:

- **Openbox** (atau DE / WM lain)
- **mpg123** (pemutar audio CLI)
- **xev** (untuk mengetahui nama tombol / keybind)
- File audio (`.wav`, `.mp3`)

> ⚠️ **PENTING**
> - Perintah instalasi **menyesuaikan distro Linux masing-masing**
> - Pengaturan shortcut **menyesuaikan DE / WM yang digunakan**
>   - Openbox → `rc.xml`
>   - GNOME / KDE → Settings → Keyboard Shortcuts
>   - i3 / bspwm / sway → config file masing-masing

---

## 🚀 Instalasi

### 1. Download sound effect

Beberapa website gratis untuk sound effect (cocok untuk soundboard):

Mixkit
https://mixkit.co/free-sound-effects/

Pixabay Sound Effects
https://pixabay.com/sound-effects/

Freesound
https://freesound.org

Y2Mate
https://v6.www-y2mate.com/

Zapsplat
https://www.zapsplat.com

SoundJay
https://www.soundjay.com/

### 2. Install paket (Arch)
```bash
sudo pacman -S mpg123 xorg-xev
```

> Untuk distro lain (Ubuntu, Fedora, dll), silakan sesuaikan package manager masing-masing.

### 3. Buat folder soundboard
```bash
mkdir -p ~/.streamdeck/sounds
```

### 4. Masukkan file suara
```bash
cp $HOME/Downloads/*.mp3 ~/.streamdeck/sounds/
```


## 5. Mengetahui Nama Keybind dengan xev

Gunakan `xev` untuk mengetahui **nama tombol (keysym)** yang akan dipakai sebagai keybind.

### Cara penggunaan
Jalankan perintah berikut di terminal:

```bash
xev | grep keysym
```

Lalu tekan tombol keyboard yang ingin digunakan.

Contoh output:
```
state 0x0, keycode 36 (keysym 0xff0d, Return), same_screen YES
```

### Penjelasan
- **`Return`** → inilah **nama keybind** yang digunakan
- `keycode 36` → kode internal keyboard
- `state 0x0` → status modifier (tidak terlalu penting)

📌 **Yang dipakai sebagai keybind adalah nama setelah koma**, yaitu:
```
Return
```

## 6. Tambahkan Keybind Openbox

Edit file:
```bash
sudo nano ~/.config/openbox/rc.xml
```

Contoh konfigurasi soundboard:

```xml
<keybind key="Return">
  <action name="Execute">
    <command>mpg123 ~/.streamdeck/aduh.mp3</command>
  </action>
</keybind>

<keybind key="1">
  <action name="Execute">
    <command>mpg123 ~/.streamdeck/BESI.mp3</command>
  </action>
</keybind>
```

> Jika menggunakan **DE / WM lain**, cukup ambil konsep keybind-nya dan sesuaikan dengan sistem masing-masing.

### 5. Reload WM / DE
```bash
openbox --reconfigure
```

Atau logout/login ulang sesuai DE / WM yang digunakan.

---

## 🧠 Cara Kerja

Setiap tombol keyboard di-bind untuk menjalankan perintah **mpg123** yang memutar file suara tertentu.

Mirip konsep tombol Stream Deck:
> Tekan tombol → aksi langsung dijalankan

---

## 🧪 Tips & Best Practice

- Gunakan **sound pendek** agar respons cepat
- Hindari konflik shortcut dengan aplikasi lain
- Bisa digabung dengan:
  - Script bash
  - OBS hotkey
  - Macro keyboard

---

## 🛠️ Contoh Script Bash (Opsional)

### Random soundboard
```bash
#!/bin/bash
SOUNDS=(~/.streamdeck/sounds/*.mp3)
mpg123 "${SOUNDS[RANDOM % ${#SOUNDS[@]}]}"
```

---

## 🖥️ Cocok Untuk

- Openbox
- WM minimalis
- Laptop low resource
- Streaming Linux
- Soundboard tanpa hardware

---

## 📜 Lisensi

Masukkan teks...

---

## ⭐ Catatan

Project ini meniru **konsep Stream Deck** dengan:
- Shortcut keyboard
- Eksekusi instan
- Tanpa GUI
- Ringan & fleksibel

---

Hatur nuhun🎧🔥
