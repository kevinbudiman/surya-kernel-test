# surya kernel — uji perbaikan storm IRQ bq2597x

Build kernel LineageOS untuk POCO X3 NFC (`surya`, branch `lineage-22.2`) di
GitHub Actions, memakai config yang diambil langsung dari HP (`/proc/config.gz`
→ `surya_running.config`).

Dua varian per build:

| Varian | Isi |
|---|---|
| `stock` | tanpa perubahan — kontrol, membuktikan toolchain menghasilkan kernel yang boot |
| `vbatmask` | `bq2597x_init_int_src()`: tambah `VBAT_INSERT` ke mask alarm `REG_0F` |

Latar belakang: setiap kali HP masuk suspend dengan kabel dicabut, `bq2597x`
mengirim interrupt dengan `INT_FLAG=0x02` (bit `VBAT_INSERT`) yang langsung
membangunkan HP, ±40 kali per menit. Bit itu satu-satunya alarm yang tidak di-mask
driver.

Jalankan: tab **Actions** → *build surya kernel* → **Run workflow**.
Hasil: artifact `surya-stock` dan `surya-vbatmask` berisi `Image.gz`.

Ini eksperimen pribadi, bukan kernel rilis.
