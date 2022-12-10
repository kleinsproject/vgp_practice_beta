<template>
  <div
    class="card-container"
    :class="{ selected: selected, dragged: dragged }"
    @click="onClick"
    @drag="dragStart"
    @dragend="dragEnd"
  >
    <div v-show="isFront" class="card_front">
      <img :src="imageFrontUrl" alt="" class="card_front_img" />
    </div>
    <div v-show="!isFront" class="card_back">
      <img :src="imageBackUrl" alt="" class="card_back_img" />
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
    imageFrontUrl: {},
    imageBackUrl: {},
    isFront: {
      default: true,
      type: Boolean,
    },
  },
  data() {
    return {
      selected: false,
      dragged: false,
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
    dragStart() {
      this.dragged = true
    },
    dragEnd() {
      this.dragged = false
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
  user-select: none;
}

.card_front,
.card_back {
  position: relative;
  width: 100%;
  height: 100%;
}
.card_front .card_front_img,
.card_back .card_back_img {
  width: 120px;
  height: 170px;
}

.selected {
  border: 1px solid blue;
  background-color: #ddf;
}
.dragged {
  opacity: 0.1;
  background-color: #dcdcdc;
}
.dragged {
  opacity: 0.1;
  background-color: #dcdcdc;
}
</style>
