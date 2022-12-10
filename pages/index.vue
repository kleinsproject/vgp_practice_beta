<template>
  <div>
    <GameField ref="child" />
    <GameCommandPalette @doCommand="doCommand" />
    <GameSidebar />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  methods: {
    doCommand(functionName) {
      this.$refs.child[functionName]()
    },
  },
}
</script>

<style>
div {
  display: flex;
}
</style>
