<template>
  <div>
    <p>場</p>
    <draggable
      :list="cards"
      id="field-container"
      :options="{ animation: 200, delay: 100 }"
    >
      <GameCard
        v-for="(card, index) in cards"
        :key="card.id"
        :cardId="card.id"
        :frontMainValue="card.frontMainValue"
        :frontSubValue="card.frontSubValue"
        :backMainValue="card.backMainValue"
        :backSubValue="card.backSubValue"
        :imageUrl="card.imageUrl"
        :isFront="card.isFront"
        :order="index"
        @add-selected-array="addSelectedArray"
        @remove-selected-array="removeSelectedArray"
        class="margin"
      />
    </draggable>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
export default {
  components: {
    draggable,
  },
  data() {
    return {
      selectedCards: [],
      returnCards: [],
      decks: [
        {
          id: 1,
        },
      ],
      cards: [
        {
          id: 1,
          frontMainValue: 10,
          frontSubValue: 'heart',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust1.png'),
          isFront: true,
        },
        {
          id: 2,
          frontMainValue: 8,
          frontSubValue: 'dia',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust2.png'),
          isFront: true,
        },
        {
          id: 3,
          frontMainValue: 'K',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust3.png'),
          isFront: true,
        },
        {
          id: 4,
          frontMainValue: 'A',
          frontSubValue: 'clover',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust4.png'),
          isFront: true,
        },
        {
          id: 5,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust5.png'),
          isFront: true,
        },
        {
          id: 6,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust6.png'),
          isFront: true,
        },
        {
          id: 7,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageUrl: require('@/static/image/torannpu-illust7.png'),
          isFront: true,
        },
      ],
    }
  },
  methods: {
    addSelectedArray(id) {
      console.log(id)
      this.selectedCards.push(id)
    },
    removeSelectedArray(id) {
      this.selectedCards = this.selectedCards.filter((card) => card !== id)
    },
    turn() {
      this.returnCards = this.cards.filter((card) =>
        this.selectedCards.includes(card.id)
      )
      for (const card of this.returnCards) {
        card.isFront = !card.isFront
      }
    },
  },
}
</script>
<style scoped>
#field-container {
  position: fixed;
  top: 0;
  left: 200px;
  width: calc(100% - 260px);
  margin: 30px;
  padding: 50px;
  height: 70vh;
  border: 1px solid #000;
  box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
}
.margin {
  margin: 10px;
}
.sortable-chosen {
  opacity: 0.1;
  background-color: #dcdcdc;
}
.sortable-ghost {
  opacity: 0.1;
  background-color: #dcdcdc;
}
</style>
