# Dicoding Belajar Fundamental Generative AI

Project ini merupakan submission untuk kelas **Belajar Fundamental Generative AI**. Fokus utamanya adalah membangun alur **image generation** dan **image editing** berbasis **Stable Diffusion**, lalu menyediakan antarmuka interaktif menggunakan **Streamlit**.

Di dalam project ini terdapat dua bagian utama:

- **Notebook pipeline** untuk mengerjakan eksperimen inti seperti text-to-image, base + refiner, inpainting, automasking, outpainting, dan zoom out.
- **Aplikasi Streamlit** untuk mendemonstrasikan alur generasi gambar dan editing gambar secara interaktif.

![Penilaian Proyek](README/penilaian_proyek.png)

## Fitur Utama

- **Text-to-Image** menggunakan `StableDiffusionPipeline`
- Pengaturan **guidance scale**, **inference steps**, **seed**, dan **scheduler**
- **Batch image generation**
- **Inpainting** dengan masking manual
- **Inpainting dengan automasking** berbasis model segmentation
- **Outpainting** untuk memperluas gambar ke satu arah
- **Zoom Out outpainting** untuk memperluas gambar bertahap ke beberapa arah
- **Base + Refiner pattern logic** dengan pendekatan two-stage generation pada Stable Diffusion v1.5
- Antarmuka **Streamlit** untuk generate dan edit gambar

## Demo Aplikasi

Preview cara kerja aplikasi dapat dilihat pada video berikut:

[Lihat video demo Streamlit](readme/video_demo_aplikasi_BFGAI_Muhammad%20Abiya%20Makruf.mp4)

## Teknologi yang Digunakan

- Python 3.12
- PyTorch
- Diffusers
- Transformers
- Streamlit
- streamlit-drawable-canvas
- Pyngrok
- Matplotlib
- Pillow

## Cara Menjalankan Program

### 1. Clone repository dan masuk ke folder project

```bash
git clone <url-repository>
cd Dicoding-BelajarFundamentalGenerativeAI
```

### 2. Install dependency

Jika menggunakan `uv`:

```bash
uv sync
```

Jika menggunakan `pip`:

```bash
pip install -r requirements.txt
```

### 3. Jalankan aplikasi Streamlit secara lokal

```bash
streamlit run streamlit_app/app.py
```

Setelah itu buka browser ke alamat:

```text
http://localhost:8501
```

Catatan:
- Menjalankan secara lokal **tidak membutuhkan ngrok**.
- Model Stable Diffusion akan diunduh saat pertama kali dijalankan jika belum ada di cache.
- Penggunaan GPU sangat disarankan agar inferensi lebih cepat.

## Cara Menjalankan dari Notebook Streamlit

Notebook disiapkan untuk menjalankan aplikasi lewat notebook dan membagikan akses menggunakan `ngrok`.

Langkahnya:

1. Jalankan cell import dan setup dependency.
2. Jalankan cell yang menulis file `app.py` dan `logic.py` bila mengikuti alur notebook.
3. **Buat akun Ngrok** di https://ngrok.com/ jika belum punya.
4. Setelah login, buka halaman dashboard Ngrok dan salin **Authtoken** milik Anda.
5. Masukkan token tersebut ke cell autentikasi di notebook, menggantikan nilai placeholder:

```python
auth_token = "ISI_TOKEN_NGROK_ANDA"

ngrok.set_auth_token(auth_token)
subprocess.Popen(["streamlit", "run", "app.py"])
```

6. Jalankan cell tersebut untuk menyalakan server Streamlit.
7. Jalankan cell berikutnya untuk membuat public URL:

```python
public_url = ngrok.connect(8501).public_url
print(public_url)
```

8. Buka URL yang muncul untuk melihat aplikasi Streamlit dari browser.

## Kenapa Harus Membuat Token Ngrok di Notebook

Pada notebook Streamlit, `ngrok` digunakan untuk membuat **tunnel** dari port lokal Streamlit ke internet. Supaya tunnel ini bisa dibuat, Anda perlu menghubungkan sesi notebook ke akun Ngrok menggunakan **Authtoken**.

Tanpa token tersebut:

- tunnel publik tidak bisa dibuat dengan benar
- aplikasi tidak bisa diakses lewat link publik
- proses deployment dari notebook menjadi tidak lengkap

Jadi, jika aplikasi dijalankan dari notebook dan ingin dibuka melalui public URL, Anda **harus** membuat akun Ngrok lalu mengisi token Ngrok pada cell autentikasi.

## Alur Singkat Penggunaan Aplikasi

1. Masukkan prompt pada tab **Generate**.
2. Atur parameter seperti steps, CFG, seed, scheduler, dan batch size.
3. Generate gambar.
4. Pilih hasil gambar yang ingin diedit.
5. Gunakan tab **Edit** untuk melakukan inpainting atau outpainting.

## Catatan

- Beberapa model membutuhkan VRAM yang cukup besar.
- Jika terjadi error memori, gunakan fitur **Flush RAM** pada aplikasi atau restart kernel.
- Untuk penggunaan notebook berbasis cloud atau environment terisolasi, pastikan semua dependency telah terpasang sebelum menjalankan aplikasi.
