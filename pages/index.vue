<template>
  <div>
    <GameField ref="child" />
    <GameCommandPalette @turn="turn" />
    <GameSidebar />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  methods: {
    turn() {
      this.$refs.child.turn()
    },
  },
}
</script>

<style>
div {
  display: flex;
}
</style>
