<template>
  <div id="command-palette-container">
    <div v-for="command in commands" :key="command.id" class="command-button">
      {{ command.name }}
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      commands: [
        { id: 1, name: '裏返す', functionName: 'turn' },
        { id: 2, name: '移動する', functionName: 'move' },
        { id: 3, name: 'シャッフル', functionName: 'shuffle' },
        { id: 4, name: 'リセット', functionName: 'reset' },
        { id: 5, name: '裏返す', functionName: 'turn' },
      ],
    }
  },
}
</script>
<style scoped>
#command-palette-container {
  position: fixed;
  bottom: 0;
  left: 250px;
  width: calc(100% - 360px);
  margin: 30px;
  height: 20vh;
  border: 1px solid #000;
  box-sizing: border-box;
  display: flex;
  flex-wrap: nowrap;
  overflow: scroll;
  align-items: center;
}
.command-button {
  min-width: 200px;
  height: 50px;
  border: 1px solid #000;
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.command-button:hover {
  border: 1px solid red;
}
</style>
