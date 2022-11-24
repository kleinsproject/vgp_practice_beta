<template>
  <div class="card-container" :class="{ clicked: clicked }">
    <div v-show="!clicked" class="card_front" @click="onClickFront">
      <!-- <p class="card_front_main-value" v-cloak>{{ frontMainValue }}</p>
      <p class="card_front_sub-value">{{ frontSubValue }}</p> -->
      <img :src="imageUrl" alt="" />
    </div>
    <div v-show="clicked" class="card_back" @click="onClickBack">
      <p class="card_back_main-value">{{ backMainValue }}</p>
      <p class="card_back_sub-value">{{ backSubValue }}</p>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    cardId: {
      Type: Number,
    },
    frontMainValue: {
      Type: String,
    },
    frontSubValue: {
      Type: String,
    },
    backMainValue: {
      Type: String,
    },
    backSubValue: {},
    imageUrl: {},
  },
  data() {
    return {
      clicked: false,
      explanation: 'トランプ、ハートの10です',
    }
  },
  methods: {
    onClickFront() {
      this.clicked = true
      this.$emit('add-selected-array', this.cardId)
    },
    onClickBack() {
      this.clicked = false
      this.$emit('remove-selected-array', this.cardId)
    },
  },
}
</script>
<style scoped>
.card-container {
  width: 113px;
  height: 160px;
  /* margin: 20px; */
  /* border: 1px solid #000; */
  box-sizing: border-box;
}

.card_front,
.card_back {
  position: relative;
  width: 100%;
  height: 100%;
}
.card_front_main-value,
.card_back_main-value {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
}
.card_front_sub-value,
.card_back_sub-value {
  position: absolute;
  top: 10%;
  left: 10%;
  margin: 0;
}
.clicked {
  border: 1px solid blue;
  background-color: #ddf;
}
</style>
