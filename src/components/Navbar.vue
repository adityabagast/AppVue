<script setup>
import { ref } from 'vue'
import MainHome from './Home.vue'
import MainAbout from './About.vue'
import MainProjects from './Projects.vue'
import MainContact from './Contact.vue'

defineOptions({
  name: 'MainNavbar'
})

import { defineEmits } from 'vue'

const emit = defineEmits(['select-component'])

// Menambahkan state untuk mengontrol menu
const isMenuOpen = ref(false);

const selectComponent = (component) => {
  emit('select-component', component)
  isMenuOpen.value = false; // Menutup menu saat pilihan diklik
}
</script>

<template>
  <nav class="navbar">
    <div class="logo">My Portfolio</div>
    <button class="menu-toggle" @click="isMenuOpen = !isMenuOpen">
      <span class="menu-icon">☰</span>
    </button>
    <ul class="nav-links" :class="{ 'active': isMenuOpen }">
      <li><a @click.prevent="selectComponent(MainHome)">Home</a></li>
      <li><a @click.prevent="selectComponent(MainAbout)">About</a></li>
      <li><a @click.prevent="selectComponent(MainProjects)">Projects</a></li>
      <li><a @click.prevent="selectComponent(MainContact)">Contact</a></li>
    </ul>
  </nav>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  background-color: #1a1a1a; /* Warna latar belakang gelap */
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); /* Bayangan */
  position: sticky; /* Menempel di bagian atas saat scrolling */
  top: 0;
  z-index: 1000; /* Agar navbar di atas konten lain */
  border-radius: 5rem;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

.logo {
  color: #ffffff;
  font-size: 1.8rem; /* Ukuran font untuk logo */
  font-weight: bold; /* Menebalkan teks logo */
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 2rem; /* Jarak antar tautan */
}

.nav-links li a {
  color: #ffffff;
  text-decoration: none;
  padding: 0.5rem 0; /* Padding untuk tautan */
  transition: color 0.3s, border-bottom 0.3s; /* Transisi halus */
  margin-left: 1rem;
}

.nav-links li a:hover {
  color: #ffcc00; /* Warna saat hover */
  border-bottom: 2px solid #ffcc00; /* Garis bawah saat hover */
}

/* Responsivitas */
.menu-toggle {
  display: none; /* Sembunyikan tombol menu pada layar besar */
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

@media (max-width: 768px) {
  .nav-links {
    display: none; /* Sembunyikan tautan secara default */
    flex-direction: column; /* Menumpuk tautan */
    width: 100%; /* Lebar penuh */
    position: absolute; /* Menggunakan posisi absolut */
    top: 100%; /* Menempatkan di bawah navbar */
    left: 0;
    background-color: #1a1a1a; /* Warna latar belakang sama */
    padding: 1rem 0; /* Padding vertical */
    border-radius: 1rem;
    opacity: 0; /* Memulai dengan opacity 0 untuk animasi */
    transition: opacity 0.3s ease; /* Animasi untuk membuka/menutup */
    pointer-events: none; /* Mencegah interaksi saat tidak terlihat */
  }

  .nav-links.active {
    display: flex; /* Tampilkan tautan saat menu dibuka */
    opacity: 1; /* Opacity saat terlihat */
    pointer-events: auto; /* Mengizinkan interaksi saat terlihat */
  }

  .menu-toggle {
    display: block; /* Tampilkan tombol menu pada layar kecil */
  }
}
</style>
