# **Game Tic-Tac-Toe dengan Vue.js 🎮**

Ini adalah proyek game Tic-Tac-Toe klasik yang dibangun sepenuhnya menggunakan **Vue.js 3** dan **Vite**. Proyek ini dibuat sebagai latihan untuk memahami dan menerapkan konsep-konsep inti Vue seperti state management reaktif dengan Composition API, event handling, dan conditional rendering.

![Screenshot Gameplay Tic-Tac-Toe](https://i.imgur.com/g0V3hYg.png)

---

## **Fitur Utama ✨**

- **Gameplay Klasik:** Aturan permainan Tic-Tac-Toe yang standar.
- **Antarmuka Modern:** Desain yang bersih, minimalis, dan *user-friendly* dengan animasi yang halus.
- **Reaktif:** Papan permainan dan status game diperbarui secara *real-time* tanpa perlu me-refresh halaman.
- **Indikator Status:** Pesan yang jelas untuk menunjukkan giliran pemain, pemenang, atau kondisi seri.
- **Deteksi Kemenangan:** Sistem secara otomatis mendeteksi 8 kemungkinan kombinasi kemenangan dan kondisi seri.
- **Tombol Reset:** Memungkinkan pemain untuk memulai permainan baru dengan mudah setelah game berakhir.

---

## **Teknologi yang Digunakan 🛠️**

- **[Vue.js 3](https://vuejs.org/):** Menggunakan **Composition API** (`<script setup>`) untuk logika dan state management yang lebih terstruktur.
- **[Vite](https://vitejs.dev/):** Sebagai *build tool* dan *development server* yang sangat cepat.
- **HTML5 & CSS3:** Untuk struktur dan styling, termasuk penggunaan CSS Variables untuk tema yang mudah diubah.

---

## **Instalasi dan Menjalankan Proyek 🚀**

Untuk menjalankan proyek ini di komputermu, ikuti langkah-langkah berikut:

1.  **Clone repository ini (atau download ZIP):**
    ```bash
    git clone [https://github.com/URL-ANDA/tictactoe-vue.git](https://github.com/URL-ANDA/tictactoe-vue.git)
    ```

2.  **Masuk ke direktori proyek:**
    ```bash
    cd tictactoe-vue
    ```

3.  **Instal semua dependensi yang dibutuhkan:**
    ```bash
    npm install
    ```

4.  **Jalankan development server:**
    ```bash
    npm run dev
    ```

5.  Buka browser dan kunjungi `http://localhost:5173` (atau alamat lain yang muncul di terminal).

---

## **Struktur & Logika Sistem 🧠**

Seluruh sistem permainan ini terkandung dalam satu komponen Vue utama, yaitu `src/App.vue`, yang dibagi menjadi tiga bagian utama:

1.  **`<script setup>` (Logika):**
    - Berfungsi sebagai **otak** dari permainan.
    - Mengelola semua *state* (data inti) seperti `board`, `player`, dan `winner` menggunakan `ref()` dari Vue.
    - Berisi semua fungsi yang mengatur alur permainan, seperti `makeMove()`, `checkWinner()`, dan `resetGame()`.

2.  **`<template>` (Tampilan):**
    - Berfungsi sebagai **wajah** atau antarmuka visual dari permainan.
    - Menggunakan direktif Vue (seperti `v-for`, `v-if`, `@click`) untuk "menggambar" *state* menjadi elemen HTML yang bisa dilihat dan diinteraksikan oleh pengguna.

3.  **`<style>` (Gaya):**
    - Berfungsi sebagai **pakaian** dari permainan.
    - Berisi semua kode CSS yang memberikan tampilan modern, warna, layout, dan animasi pada game.

Logika inti berjalan berdasarkan **reaktivitas**. Setiap kali pemain mengklik sebuah sel, *state* `board` diperbarui. Vue secara otomatis mendeteksi perubahan ini dan langsung memperbarui tampilan di layar serta mengecek kondisi kemenangan.

---

## **Rencana Pengembangan 🎯**

Beberapa fitur yang bisa ditambahkan di masa depan:

- [ ] Papan skor untuk melacak kemenangan 'X' dan 'O'.
- [ ] Pilihan untuk bermain melawan komputer (AI sederhana).
- [ ] Pilihan tema (misalnya *dark/light mode*).
- [ ] Histori langkah dan tombol *undo*.