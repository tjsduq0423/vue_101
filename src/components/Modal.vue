<template>
  <div class="black-bg" v-if="모달창열렸니">
    <div class="white-bg">
      <img :src="모달.image" class="room-img" />
      <h4>{{ 모달.title }}</h4>
      <p>{{ 모달.content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <input v-model="month" />
      <!-- *** form validation -->
      <p>{{ month }}개월 선택함 {{ 모달.price * month }} 원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    month(post) {
      if (isNaN(post)) {
        alert("숫자를 입력해주세요.");
        this.month = 1;
      }
    },
  },
  props: {
    모달: Object,
    모달창열렸니: Boolean,
  },
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>