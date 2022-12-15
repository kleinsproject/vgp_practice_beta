<template>
  <div>
    <div class="area-container">
      <GameField
        v-for="area in areas"
        ref="child"
        :key="area.id"
        :area-num="area.id"
        class="area"
        :class="{ selected: area.selected }"
        @enable-transition="enableTransition"
        @disable-transition="disableTransition"
        @click.native="selected(area)"
      />
    </div>
    <GameCommandPalette @doCommand="doCommand" />
    <GameSidebar />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  methods: {
    doCommand(functionName) {
      for (const id of this.selectedAreaIds) {
        this.$refs.child[id - 1][functionName]()
      }
    },
    enableTransition() {
      for (let i = 0; i < this.areas.length; i++) {
        this.$refs.child[i].enableTransition()
      }
    },
    disableTransition() {
      for (let i = 0; i < this.areas.length; i++) {
        this.$refs.child[i].disableTransition()
      }
    },
    selected(area) {
      const id = area.id
      if (!this.selectedAreaIds.includes(id)) {
        this.selectedAreaIds.push(id)
        area.selected = true
      } else {
        this.selectedAreaIds = this.selectedAreaIds.filter(
          (cardId) => cardId !== id
        )
        area.selected = false
      }
    },
  },
  data() {
    return {
      isTransition: true,
      areas: [
        { id: 1, selected: false },
        { id: 2, selected: false },
        { id: 3, selected: false },
        { id: 4, selected: false },
      ],
      selectedAreaIds: [],
    }
  },
}
</script>

<style>
.area-container {
  position: absolute;
  top: 0;
  left: 260px;
  display: flex;
  flex-wrap: wrap;
}
.area {
  flex-wrap: nowrap;
  width: calc((100% - 260px) / 2);
  height: calc(40vh - 90px);
  margin: 30px;
  overflow-x: scroll;
  transition: 0.3s;
}

.selected {
  box-shadow: 0 0 2px 3px rgba(255, 100, 100, 0.3);
}
</style>
