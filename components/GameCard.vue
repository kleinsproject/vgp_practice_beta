<template>
  <div class="card-container" :class="{ selected: selected }" @click="onClick">
    <div v-show="isFront" class="card_front">
      <!-- <p class="card_front_main-value" v-cloak>{{ frontMainValue }}</p>
      <p class="card_front_sub-value">{{ frontSubValue }}</p> -->
      <img :src="imageUrl" alt="" />
    </div>
    <div v-show="!isFront" class="card_back">
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
    isFront: {
      default: true,
      type: Boolean,
    },
  },
  data() {
    return {
      selected: false,
      explanation: 'トランプ、ハートの10です',
    }
  },
  methods: {
    onClick() {
      if (this.selected) {
        this.$emit('remove-selected-array', this.cardId)
        this.selected = false
      } else if (!this.selected) {
        this.$emit('add-selected-array', this.cardId)
        this.selected = true
      }
    },
  },
}
</script>
<style scoped>
.card-container {
  border: 1px solid rgba(0, 0, 0, 0);
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
.selected {
  border: 1px solid blue;
  background-color: #ddf;
}
</style>
