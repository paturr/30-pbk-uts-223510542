<template>
    <div class="about-container">
      <div class="about-content">
        <h1 class="about-title">Tentang Saya</h1>
        <p class="about-description">Saya merupakan mahasiswa Universitas Islam Riau dengan program studi Teknik Informatika. Sekarang saya tengah berada di smester 4, ditengah kesibukan kuliah saya, Saya sangat gemar bermain game online, diantaranya adalah seperti eFootbal 2022, PUBG Mobile, Mobile Legends dan masih banyak lagi yang lain.</p>
        <button class="home-button" @click="goHome">Kembali ke Beranda</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      goHome() {
        this.$router.push('/');
      }
    }
  }
  </script>
  
  <style scoped>
  .about-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #ffffff;
    background-image: url('https://i.pinimg.com/originals/7b/55/b4/7b55b4f2f9453b99b0f8a1e896f6d795.jpg');
    background-size: cover;
    background-position: center;
    padding: 20px;
  }
  
  .about-content {
    text-align: center;
    background: rgba(0, 0, 0, 0.8);
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    animation: fadeIn 2s ease-in-out;
  }
  
  .about-title {
    font-size: 40px;
    font-weight: bold;
    color: #0b0006;
    margin-bottom: 20px;
    animation: slideIn 1s ease-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .about-description {
    font-size: 20px;
    color: #fff;
    margin-bottom: 30px;
    animation: fadeInUp 1.5s ease-in-out;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .home-button {
    padding: 10px 20px;
    font-size: 18px;
    color: #fff;
    background-color: #000000;
    border: none;
    border-radius: 20px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.3s;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }
  
  .home-button:hover {
    background-color: #000000;
    transform: scale(1.1);
  }
  
  @keyframes fadeIn {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }
  
  @keyframes slideIn {
    0% { transform: translateY(-20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
  
  @keyframes fadeInUp {
    0% { transform: translateY(20px); opacity: 0; }
    100% { transform: translateY(0); opacity: 1; }
  }
  </style>
  