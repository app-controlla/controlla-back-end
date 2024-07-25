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
          <i :class="themeIcon"></i>
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
  data() {
    return {
      darkMode: false,
    };
  },
  computed: {
    themeIcon() {
      return this.darkMode ? 'fas fa-sun' : 'fas fa-moon';
    },
  },
  created() {
    const savedTheme = localStorage.getItem('darkMode');
    if (savedTheme !== null) {
      this.darkMode = savedTheme === 'true';
    }
    if (this.darkMode) {
      document.body.classList.add('dark-mode');
    } else {
      document.body.classList.add('light-mode');
    }
  },
  methods: {
    toggleTheme() {
      this.darkMode = !this.darkMode;
      if (this.darkMode) {
        document.body.classList.add('dark-mode');
        document.body.classList.remove('light-mode');
      } else {
        document.body.classList.remove('dark-mode');
        document.body.classList.add('light-mode');
      }
      localStorage.setItem('darkMode', this.darkMode);
    },
  },
};
</script>

<style scoped>
@import './assets/css/style.css';
</style>
