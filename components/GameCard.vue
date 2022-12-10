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
  width: fit-content;
  height: fit-content;
  /* transition: all 0.5s, border 0.05s; */
  box-sizing: border-box;
  user-select: none;
}

.card_front,
.card_back {
  position: relative;
}
.card_front .card_front_img,
.card_back .card_back_img {
  width: 120px;
  height: 170px;
}

.selected {
  box-shadow: 0 0 2px 3px rgba(100, 100, 255, 0.3);
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
