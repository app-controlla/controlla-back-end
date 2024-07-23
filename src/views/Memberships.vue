<template>
    <div>
      <div id="membershipModal" class="modal" v-show="isModalVisible">
        <div class="modal-content">
          <span class="close-button" @click="closeModal">&times;</span>
          <form @submit.prevent="submitMembership">
            <label for="membershipName">Name:</label>
            <input type="text" v-model="newMembership.name" id="membershipName"><br><br>
            <label for="membershipValue">Value:</label>
            <input type="text" v-model="newMembership.value" id="membershipValue"><br><br>
            <label for="membershipImage">Image URL:</label>
            <input type="text" v-model="newMembership.imageUrl" id="membershipImage"><br><br>
            <label for="membershipColor">Background Color:</label>
            <input type="color" v-model="newMembership.color" id="membershipColor"><br><br>
            <input type="submit" value="Submit">
          </form>
        </div>
      </div>
      <div class="membership-page">
        <h1>Memberships</h1>
        <p>Here you can manage your memberships.</p>
        <div class="membership-cards-container" id="membershipContainer">
          <div v-for="membership in memberships" :key="membership._id" class="membership-card work">
            <div class="membership-img-section">
              <img v-if="membership.imageUrl" :src="membership.imageUrl" alt="Membership" style="width:100%;">
              <div v-else :style="{ backgroundColor: membership.color || 'hsla(0, 0%, 0%, 0)', height: '100px', borderRadius: '10px' }"></div>
            </div>
            <div class="membership-card-desc">
              <div class="membership-card-header">
                <div class="membership-card-title">{{ membership.name }}</div>
                <div class="membership-card-menu">
                  <div class="membership-dot"></div>
                  <div class="membership-dot"></div>
                  <div class="membership-dot"></div>
                </div>
              </div>
              <div class="membership-card-time">{{ membership.value }}</div>
            </div>
          </div>
        </div>
        <button id="addMembershipButton" class="add-membership-button" @click="openModal">
          <ion-icon name="add"></ion-icon>
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isModalVisible: false,
        memberships: [],
        newMembership: {
          name: '',
          value: '',
          imageUrl: '',
          color: ''
        }
      };
    },
    methods: {
      openModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      },
      async fetchMemberships() {
        try {
          const response = await fetch('http://localhost:3000/api/memberships');
          this.memberships = await response.json();
        } catch (error) {
          console.error('Error fetching memberships:', error);
        }
      },
      async submitMembership() {
        try {
          await fetch('http://localhost:3000/api/memberships', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(this.newMembership),
          });
          this.fetchMemberships();
          this.closeModal();
          this.newMembership = { name: '', value: '', imageUrl: '', color: '' };
        } catch (error) {
          console.error('Error adding membership:', error);
        }
      }
    },
    mounted() {
      this.fetchMemberships();
    }
  };
  </script>
  
  <style scoped>
  .membership-page {
    padding: 20px;
  }
  
  .add-membership-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    font-size: 24px;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .add-membership-button ion-icon {
    font-size: inherit;
  }
  
  .modal {
    display: none;
  }
  
  .modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 80%;
  }
  
  .close-button {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }
  
  .close-button:hover,
  .close-button:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
  
  .membership-cards-container {
    display: flex;
    flex-wrap: wrap;
    gap: 50px;
  }
  
  .membership-card {
    --primary-clr: var(--blue);
    --dot-clr: #BBC0FF;
    --play: hsl(195, 74%, 62%);
    width: 300px;
    height: 170px;
    border-radius: 10px;
    color: #fff;
    display: grid;
    cursor: pointer;
    grid-template-rows: 50px 1fr;
    position: relative;
    padding: 20px;
    background: var(--primary-clr);
  }
  
  .membership-card.work {
    border-radius: 10px;
  }
  
  .membership-card:hover .membership-img-section {
    transform: translateY(1em);
  }
  
  .membership-card-desc {
    border-radius: 10px;
    padding: 15px;
    position: relative;
    top: -10px;
    display: grid;
    gap: 10px;
    background: var(--primary-clr);
  }
  
  .membership-card-time {
    font-size: 1.7em;
    font-weight: 500;
  }
  
  .membership-img-section {
    transition: 0.2s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    background: hsla(195, 74%, 62%, 0); /* Fully transparent */
  }
  
  .membership-card-header {
    display: flex;
    align-items: center;
    width: 100%;
  }
  
  .membership-card-title {
    flex: 1;
    font-size: 0.9em;
    font-weight: 500;
  }
  
  .membership-card-menu {
    display: flex;
    gap: 4px;
    margin-inline: auto;
  }
  
  .membership-dot {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: var(--dot-clr);
  }
  </style>
  