<template>
  <div class="overview radial-out">
    <div class="main-img">
      <img src="../assets/chef.svg" alt="image" />
    </div>

    <a v-if="!!searchLink" :href="searchLink" target="_blank"
      >Tignan ang recipe nang matapos na to</a
    >
    <div class="result">
      <h1 :class="{ hithere: showConffeti }">
        {{ showResult ? food[randomNumber] : 'Nak, ano ulam?' }}
      </h1>
    </div>

    <button :disabled="starting" @click="start" class="start-btn">
      SAGUTIN
    </button>

    <Confetti v-if="showConffeti" />
  </div>
</template>

<script>
import { FOOD } from '../constants';
import Confetti from './Confetti.vue';

export default {
  name: 'Overview',
  components: {
    Confetti,
  },
  data() {
    return {
      food: FOOD,
      randomNumber: 0,
      showConffeti: false,
      starting: false,
      showResult: false,
      result: '',
      searchLink: '',
    };
  },
  methods: {
    start() {
      this.searchLink = '';
      this.starting = true;
      this.showResult = true;

      const interval = setInterval(() => {
        this.randomNumber = Math.floor(Math.random() * this.food.length);
        requestAnimationFrame(() => ({
          particleCount: 2,
          angle: 60,
          spread: 55,
          origin: { x: 0 },
          colors: this.colors,
        }));
      }, 70);

      setTimeout(() => {
        this.showConffeti = true;
        this.starting = false;
        this.generateLink();

        setTimeout(() => {
          this.showConffeti = false;
        }, 2500);

        clearInterval(interval);
      }, 5000);
    },
    generateLink() {
      const searchValue = this.food[this.randomNumber]
        .replace(/\s+/g, '-')
        .toLowerCase();

      this.searchLink = `https://panlasangpinoy.com/?s=${searchValue}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.overview {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 15px;
  background-color: #ff6666;

  .main-img img {
    width: 150px;
    margin-bottom: 20px;
  }

  .result {
    text-align: center;
    height: 90px;
    color: #fff;
  }

  .start-btn {
    padding: 10px;
    font-size: 20px;
    font-weight: bold;
    border-radius: 50%;
    height: 5;
    border: 0;
    width: 120px;
    height: 120px;
    cursor: pointer;
    margin-top: 20px;
    background-color: #fff;
    transition: 0.4s;

    &:hover {
      opacity: 0.8;
    }
  }

  a {
    text-align: center;
    margin-bottom: 20px;
    text-decoration: none;
  }
}

.hithere {
  animation: hithere 2s ease 1;
}
@keyframes hithere {
  30% {
    transform: scale(1.2);
  }
  40%,
  60% {
    transform: rotate(-20deg) scale(1.2);
  }
  50% {
    transform: rotate(20deg) scale(1.2);
  }
  70% {
    transform: rotate(0deg) scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
