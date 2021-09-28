<template>
  <!-- <div class="start" :class="{ end: 모달창열렸니 }">
    <Modal
      @closeModal="모달창열렸니 = false"
      :모달="모달"
      :모달창열렸니="모달창열렸니"
    />
  </div> -->
  <transition name="fade">
    <Modal
      @closeModal="모달창열렸니 = false"
      :모달="모달"
      :모달창열렸니="모달창열렸니"
    />
  </transition>

  <div class="menu">
    <a v-for="메뉴 in 메뉴들" :key="메뉴">{{ 메뉴 }}</a>
  </div>
  <Discount />

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <Card
    @openModal="
      모달창열렸니 = true;
      모달 = $event;
    "
    :원룸="원룸"
    v-for="원룸 in 원룸들"
    :key="원룸"
  />
</template>

<script>
import data from "./assets/oneroom.js";
import Discount from "./components/Discount.vue";
import Modal from "./components/Modal.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  data() {
    return {
      원룸들오리지널: [...data],
      모달: null,
      원룸들: [...data],
      모달창열렸니: false,
      메뉴들: ["Home", "Products", "About"],
    };
  },
  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  },
  methods: {
    priceSort() {
      this.원룸들.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
  },
};
</script>

<style>
.fade-enter-from {
  /* opacity: 0; */
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 0.5s;
}
.fade-enter-to {
  transform: translateY(0px);
}
.fade-leave-from {
  transform: translateY(0px);
}
.fade-leave-active {
  transition: all 0.5s;
}
.fade-leave-to {
  transform: translateY(-1000px);
}
/* .start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
} */
.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
