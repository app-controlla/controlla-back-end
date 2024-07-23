<template>
    <div class="navigation">
      <ul>
        <li>
          <a href="#">
            <span class="icon">
              <img src="https://raw.githubusercontent.com/westwindd/DiaDia/main/a-removebg-preview.png" alt="Controlla Logo" width="60">
            </span>
            <span class="title"><span class="brand-name">Controlla</span></span>
          </a>
        </li>
        <li>
          <button id="theme-toggle" class="theme-toggle" @click="toggleTheme">
            <i class="fas fa-moon"></i>
          </button>
        </li>
        <li class="hovered">
          <a href="#">
            <span class="icon">
              <ion-icon name="home-outline"></ion-icon>
            </span>
            <span class="title">Dashboard</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="people-outline"></ion-icon>
            </span>
            <span class="title">Membership</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="chatbubble-outline"></ion-icon>
            </span>
            <span class="title">Messages</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="help-outline"></ion-icon>
            </span>
            <span class="title">Help</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="settings-outline"></ion-icon>
            </span>
            <span class="title">Settings</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="lock-closed-outline"></ion-icon>
            </span>
            <span class="title">Password</span>
          </a>
        </li>
        <li>
          <a href="#">
            <span class="icon">
              <ion-icon name="log-out-outline"></ion-icon>
            </span>
            <span class="title">Sign Out</span>
          </a>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      toggleTheme() {
        document.body.classList.toggle('dark-mode');
        const themeToggleIcon = document.querySelector('#theme-toggle i');
        if (document.body.classList.contains('dark-mode')) {
          themeToggleIcon.classList.replace('fa-moon', 'fa-sun');
        } else {
          themeToggleIcon.classList.replace('fa-sun', 'fa-moon');
        }
      }
    }
  };
  </script>
  
  <style scoped>
  @import './assets/css/style.css';
  </style>
  