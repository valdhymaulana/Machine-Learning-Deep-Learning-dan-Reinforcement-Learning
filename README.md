# 🦾 Planar Robot 3-DOF Inverse Kinematics with AI

Proyek ini mendemonstrasikan penyelesaian masalah **Inverse Kinematics (IK)** pada robot planar 3-Degree of Freedom (3-DOF) menggunakan tiga pendekatan kecerdasan buatan: **Machine Learning (ML)**, **Deep Learning (DL)**, dan **Reinforcement Learning (RL)**.

## 🤖 Spesifikasi Robot
- **Tipe:** Planar Arm 3-Link
- **Panjang Link:** $L_1=0.5m, L_2=0.4m, L_3=0.3m$
- **Workspace:** Jangkauan maksimum 1.2 meter.
- **Joint Limits:** 
  - $\theta_1$: $\pm\pi$ (Shoulder)
  - $\theta_2$: $\pm2\pi/3$ (Elbow)
  - $\theta_3$: $\pm\pi/2$ (Wrist)

## 🚀 Fitur Utama
- **Forward Kinematics (FK):** Perhitungan posisi end-effector (x, y) dari sudut sendi.
- **Data Generation:** Pembangkitan dataset otomatis (300.000+ sampel) dengan filter stabilitas.
- **Pendekatan AI:** ML (KNN & Boosted RF), DL (PyTorch MLP), dan RL (PPO).

## 📊 Hasil Perbandingan Error

Setelah melatih semua model dengan konfigurasi link baru, berikut adalah performa masing-masing metode:

| Metode | Mean Error (cm) | Karakteristik Performa |
| :--- | :--- | :--- |
| **KNN (k=5)** | ~3.83 cm | Paling akurat pada dataset lokal, namun butuh memori besar. |
| **Random Forest** | ~7.21 cm | Sangat stabil dan handal untuk regresi multi-output. |
| **RL (PPO)** | ~11.75 cm | Menarik karena belajar tanpa dataset, namun butuh waktu training lama. |
| **Deep Learning** | >100 cm* | Sangat cepat, namun akurasi sangat bergantung pada arsitektur & loss function. |

> *Catatan: Model DL menunjukkan error tinggi pada percobaan ini karena kompleksitas pemetaan non-linear pada link yang lebih panjang, memerlukan tuning lebih lanjut pada loss function kartesian.*

### 📈 Visualisasi Error
<img width="714" height="403" alt="Screenshot 2026-06-03 115921" src="https://github.com/user-attachments/assets/5e3da25e-3288-40c9-82c6-8792653d96e3" />


*Grafik di atas menunjukkan distribusi error end-effector (dalam cm) untuk masing-masing metode.*

## 📝 Kesimpulan Analisis
1. **Peningkatan Jangkauan:** Dengan panjang link baru, area kerja robot meningkat signifikan (~77.8%).
2. **Kesesuaian Metode:** 
    - Gunakan **KNN/RF** jika akurasi pada koordinat spesifik adalah prioritas utama.
    - Gunakan **DL** untuk aplikasi yang membutuhkan prediksi real-time yang sangat ringan.
    - Gunakan **RL** jika robot harus beradaptasi dengan rintangan (obstacle avoidance) tanpa dataset eksplisit.
