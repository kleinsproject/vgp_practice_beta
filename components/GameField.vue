<template>
  <div>
    <p>場</p>
    <draggable
      v-model="cards"
      id="field_container"
      :options="{ animation: 100 }"
      @start="onStart"
      @end="onEnd"
    >
      <transition-group class="transition_container" :name="transitionName">
        <GameCard
          v-for="card in cards"
          :key="card.id"
          :cardId="card.id"
          :frontMainValue="card.frontMainValue"
          :frontSubValue="card.frontSubValue"
          :backMainValue="card.backMainValue"
          :backSubValue="card.backSubValue"
          :imageFrontUrl="card.imageFrontUrl"
          :imageBackUrl="card.imageBackUrl"
          :isFront="card.isFront"
          :order="card.order"
          @add-selected-array="addSelectedArray"
          @remove-selected-array="removeSelectedArray"
          class="margin"
        />
      </transition-group>
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
      transitionName: 'list',
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
          imageFrontUrl: require('@/static/image/torannpu-illust1.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 1,
        },
        {
          id: 2,
          frontMainValue: 8,
          frontSubValue: 'dia',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust2.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 2,
        },
        {
          id: 3,
          frontMainValue: 'K',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust3.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 3,
        },
        {
          id: 4,
          frontMainValue: 'A',
          frontSubValue: 'clover',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust4.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 4,
        },
        {
          id: 5,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust5.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 5,
        },
        {
          id: 6,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust6.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 6,
        },
        {
          id: 7,
          frontMainValue: 'Q',
          frontSubValue: 'spade',
          backMainValue: '裏',
          backSubValue: null,
          explanation: 'トランプ、ハートの10です',
          imageFrontUrl: require('@/static/image/torannpu-illust7.png'),
          imageBackUrl: require('@/static/image/card_back.jpeg'),
          isFront: true,
          order: 7,
        },
      ],
    }
  },
  methods: {
    addSelectedArray(id) {
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
    shuffle() {
      const array = Array.from(Array(this.cards.length).keys())
        .map((key) => key + 1)
        .sort((a, b) => Math.random() - 0.5)
      for (let i = 0; i < array.length; i++) {
        this.cards[i].order = array[i]
      }
      this.sort()
    },
    sort() {
      this.cards.sort((a, b) => a.order - b.order)
    },
    onStart(event) {
      event.item.classList.add('drag_ghost')
      // console.log(event.item.classList, new Date())
      this.transitionName = 'none'
    },
    onEnd(event) {
      for (let i = 0; i < this.cards.length; i++) {
        this.cards[i].order = i + 1
      }
      this.transitionName = 'list'
      event.item.classList.remove('drag_ghost')
    },
  },
}
</script>
<style scoped>
#field_container {
  padding: 20px;
  border: 1px solid #000;
  box-sizing: border-box;
}
.transition_container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 100%;
}
.list-move {
  transition: 0.5s;
}
.margin {
  margin: 10px;
  /* transition: 0.5s; */
}
</style>
