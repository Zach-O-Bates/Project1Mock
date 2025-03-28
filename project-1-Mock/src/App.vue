<template>
  <div class="app-container">
    <div class="app-bar">
      <button @click="navigateToPage('home')" class="back-button">
        <ChevronLeft class="back-arrow" />
      </button>
      <h1 class="app-title">QuickSpot</h1>
    </div>

    <div class="content">
      <div class="flex-column">
        <div v-if="currentPage === 'home'">
          <div class="user-info">
            <UserIcon class="user-icon" />
            <h2 class="user-name">USER123</h2>
          </div>

          <div class="buttons-container">
            <button 
              v-for="(button, index) in buttons" 
              :key="index" 
              @click="navigateToPage(button.action)" 
              class="button"
            >
              {{ button.text }}
            </button>
          </div>
        </div>

        <div v-if="currentPage === 'wallet'">
          <div class="wallet-header">
            <div class="wallet-title">
              <h2>Wallet</h2>
              <hr />
            </div>
          </div>

          <div class="cards-container">
            <div class="card" v-for="(card, index) in cards" :key="index">
              <div class="card-box">
                <h3>{{ card.name }}</h3>
                <p>**** **** **** {{ card.last4 }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="currentPage === 'reviews'">
          <div class="wallet-header">
            <div class="wallet-title">
              <h2>Reviews</h2>
              <hr />
            </div>
          </div>

          <div class="reviews-container">
            <div class="review-card" v-for="(review, index) in reviews" :key="index">
              <h3>{{ review.name }}</h3>
              <p>{{ review.text }}</p>
              <p><strong>Rating:</strong> {{ review.rating }} stars</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ChevronLeft } from 'lucide-vue-next';

export default {
  components: { ChevronLeft },
  data() {
    return {
      currentPage: 'home',
      buttons: [
        { text: 'Wallet', action: 'wallet' },
        { text: 'Active Reservations', action: () => alert('Active Reservations clicked') },
        { text: 'Parking History', action: () => alert('Parking History clicked') },
        { text: 'Reviews', action: 'reviews' },
      ],
      cards: [
        { name: 'Visa', last4: '1234' },
        { name: 'Mastercard', last4: '5678' },
        { name: 'Amex', last4: '9876' }
      ],
      reviews: [
        { name: 'USER123', text: 'Great parking spot, very convenient and easy to access!', rating: 5 },
        { name: 'USER123', text: 'The parking lot was a bit crowded, but overall fine.', rating: 3 },
        { name: 'USER123', text: 'Amazing location, had no trouble finding a spot. Will use again!', rating: 4 }
      ]
    };
  },
  methods: {
    navigateToPage(action) {
      if (action === 'wallet') {
        this.currentPage = 'wallet';
      } else if (action === 'reviews') {
        this.currentPage = 'reviews';
      } else if (action === 'home') {
        this.currentPage = 'home';
      } else {
        action();
      }
    }
  }
};
</script>

<style scoped>
.app-bar {
  background-color: #8EBBFF;
  color: white;
  display: flex;
  align-items: center;
  padding: 16px;
  position: relative;
}

.app-title {
  font-size: 24px;
  font-weight: 600;
  flex-grow: 1;
  text-align: center;
}

.back-button {
  background-color: transparent;
  color: white;
  font-size: 20px;
  border: none;
  cursor: pointer;
  position: absolute;
  left: 16px;
}

.back-arrow {
  width: 24px;
  height: 24px;
}

.content {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-grow: 1;
  padding: 32px;
  background-color: #24293E;
}

.flex-column {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.wallet-header {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  margin-bottom: 16px;
}

.wallet-title {
  text-align: center;
  color: white;
  margin-bottom: 16px;
}

.wallet-title h2 {
  font-size: 24px;
  font-weight: 600;
}

.wallet-title hr {
  width: 80%;
  border: 1px solid white;
  margin-top: 8px;
}

.card-box, .review-card {
  background-color: #8EBBFF;
  color: white;
  width: 300px;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 16px;
}

.card-box h3, .review-card h3 {
  font-size: 18px;
  font-weight: 600;
}

.card-box p, .review-card p {
  font-size: 16px;
  margin-top: 8px;
  font-weight: 400;
}

.reviews-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 16px;
}

.button {
  width: 100%;
  padding: 12px;
  margin-bottom: 16px;
  background-color: #8EBBFF;
  color: white;
  font-size: 16px;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  border: none;
}

.button:hover {
  background-color: #1e2531;
}

.button:active {
  background-color: #181f2a;
}
</style>

