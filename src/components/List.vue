<template>
  <div class="list">
    <div v-for="(item, index) in listItem" :key="index" v-bind:class="{ checked: item.checked }">
      <input type="checkbox" v-model="item.checked" />
      <span>{{ item.text }}</span>
      <button v-on:click="deleteItem(index)" class="button btn-delete">Remove</button>
    </div>
  </div>
</template>
  
<script>
export default {
  name: 'ListAdded',
  props: {
    listItem: { type: Array },
    deleteItem: { type: Function },
  },
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list {
  display: flex;
  flex-direction: column;
}
</style>
  