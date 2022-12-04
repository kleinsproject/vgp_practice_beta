<template>
  <div class="card-container" :class="{ selected: selected }" @click="onClick">
    <div v-show="isFront" class="card_front">
      <img :src="imageUrl" alt="" class="card_front_img" />
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
  width: fit-content;
  height: fit-content;
  /* transition: all 0.5s, border 0.05s; */
  box-sizing: border-box;
}

.card_front,
.card_back {
  position: relative;
}
.card_front .card_front_img,
.card_back {
  width: 120px;
  height: 170px;
}
.card_back_main-value {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
}
.card_back_sub-value {
  position: absolute;
  top: 10%;
  left: 10%;
  margin: 0;
}
.selected {
  box-shadow: 0 0 2px 3px rgba(100, 100, 255, 0.3);
}
</style>
