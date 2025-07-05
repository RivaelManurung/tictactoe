<script setup>
// Bagian Logika (Otak dari Game)
import { ref, computed } from 'vue'

// --- State (Data yang Perlu Diingat) ---
// Papan permainan, direpresentasikan oleh array 9 kotak. '' artinya kosong.
const board = ref(Array(9).fill(''))

// Pemain saat ini ('X' atau 'O'). Dimulai dari 'X'.
const player = ref('X')

// Pemenang game (null jika belum ada, 'X', 'O', atau 'Seri').
const winner = ref(null)

// --- Konstanta ---
// "Buku Contekkan" semua 8 kemungkinan kombinasi untuk menang.
const WINNING_COMBINATIONS = [
  [0, 1, 2], [3, 4, 5], [6, 7, 8], // Baris
  [0, 3, 6], [1, 4, 7], [2, 5, 8], // Kolom
  [0, 4, 8], [2, 4, 6]             // Diagonal
]

// --- Fungsi (Aksi yang Bisa Dilakukan) ---
// Fungsi ini dijalankan saat sebuah kotak diklik.
const makeMove = (index) => {
  // 1. Validasi: Jangan lakukan apa-apa jika game sudah selesai atau kotak sudah diisi.
  if (winner.value || board.value[index] !== '') {
    return
  }

  // 2. Aksi: Isi kotak dengan simbol pemain saat ini.
  board.value[index] = player.value

  // 3. Pengecekan: Cek apakah langkah ini menghasilkan pemenang.
  checkWinner()

  // 4. Ganti Giliran: Jika belum ada pemenang, ganti giliran pemain.
  if (!winner.value) {
    player.value = player.value === 'X' ? 'O' : 'X'
  }
}

// Fungsi untuk mengecek kondisi kemenangan atau seri.
const checkWinner = () => {
  for (const combination of WINNING_COMBINATIONS) {
    const [a, b, c] = combination
    
    // Cek jika 3 kotak dalam satu kombinasi sama dan tidak kosong.
    if (
      board.value[a] &&
      board.value[a] === board.value[b] &&
      board.value[a] === board.value[c]
    ) {
      winner.value = board.value[a] // Set pemenangnya.
      return // Hentikan pengecekan.
    }
  }

  // Jika tidak ada pemenang, cek kondisi seri (papan penuh).
  if (!board.value.includes('')) {
    winner.value = 'Seri'
  }
}

// Fungsi untuk mereset permainan ke kondisi awal.
const resetGame = () => {
  board.value = Array(9).fill('')
  player.value = 'X'
  winner.value = null
}

// --- Computed Property (Data Turunan) ---
// Pesan status yang akan otomatis berubah sesuai kondisi game.
const message = computed(() => {
  if (winner.value) {
    return winner.value === 'Seri' ? `Permainan Seri!` : `Pemenang: ${winner.value}!`
  } else {
    return `Giliran Pemain: ${player.value}`
  }
})
</script>

<template>
  <main class="app">
    <h1>Tic Tac Toe</h1>

    <h2 class="status">{{ message }}</h2>

    <div class="board">
      <div
        v-for="(cell, index) in board"
        :key="index"
        class="cell"
        @click="makeMove(index)"
        :class="`player-${cell.toLowerCase()}`"
      >
        {{ cell }}
      </div>
    </div>

    <button v-if="winner" @click="resetGame" class="reset-button">
      Mulai Lagi
    </button>
  </main>
</template>

<style>
 /* Palet Warna yang Diperbarui */
 :root {
  --primary-color: #64B5F6; /* Biru Muda */
  --secondary-color: #424242; /* Abu-abu Gelap */
  --board-bg: #E0F7FA; /* Biru Muda Sekali */
  --cell-bg: #FFF; /* Putih */
  --text-color: var(--secondary-color);
  --x-color: #EF5350; /* Merah */
  --o-color: #4CAF50; /* Hijau */
  --hover-bg: #B2EBF2; /* Biru Muda Lebih Gelap (Hover) */
  --win-color: #FFCA28; /* Kuning Emas untuk Pemenang */
 }
 
 body {
  background-color: var(--primary-color);
  color: var(--text-color);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  margin-top: 40px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
 }
 
 .app {
  background-color: var(--board-bg);
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  align-items: center;
 }
 
 h1 {
  color: var(--secondary-color);
  margin-bottom: 20px;
 }
 
 .status {
  font-size: 1.2rem;
  margin-bottom: 25px;
  font-weight: 500;
  color: var(--primary-color);
  min-height: 24px; /* Untuk mencegah perubahan layout saat status kosong */
 }
 
 .board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 8px;
  padding: 10px;
  border-radius: 8px;
  background-color: var(--primary-color); /* Warna di antara sel */
 }
 
 .cell {
  background-color: var(--cell-bg);
  border-radius: 6px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2.5rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.1s ease;
  user-select: none; /* Mencegah teks terseleksi saat klik cepat */
 }
 
 .cell:hover {
  background-color: var(--hover-bg);
  transform: scale(1.05);
 }
 
 .cell.player-x {
  color: var(--x-color);
 }
 
 .cell.player-o {
  color: var(--o-color);
 }
 
 .reset-button {
  margin-top: 30px;
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: 600;
  color: var(--cell-bg);
  background-color: var(--primary-color);
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.1s ease, box-shadow 0.3s ease;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
 }
 
 .reset-button:hover {
  background-color: #5393F4;
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
 }
 
 .reset-button:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
 }
 </style>