<template>
    <div class="topbar">
      <div class="toggle" @click="toggleSidebar">
        <ion-icon name="menu-outline"></ion-icon>
      </div>
      <div class="search">
        <ion-icon name="search-outline"></ion-icon>
        <input type="text" placeholder="Search here" />
      </div>
      <div class="user">
        <img src="assets/imgs/customer01.jpg" alt="User" />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      toggleSidebar() {
        this.$emit('toggle-sidebar');
      }
    }
  };
  </script>
  
  <style scoped>
  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    background-color: var(--white);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
  }
  
  .toggle {
    font-size: 24px;
    cursor: pointer;
  }
  
  .search {
    flex: 1;
    display: flex;
    justify-content: center;
    position: relative;
  }
  
  .search ion-icon {
    position: absolute;
    left: 10px;
    top: 50%;
    transform: translateY(-50%);
    color: #ddd;
    font-size: 20px;
  }
  
  .search input {
    width: 50%;
    max-width: 500px;
    padding: 10px 10px 10px 40px;
    border: 1px solid #ddd;
    border-radius: 20px;
    font-size: 16px;
    outline: none;
  }
  
  .user {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    overflow: hidden;
    cursor: pointer;
  }
  
  .user img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  </style>
  