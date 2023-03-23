<template>
  <div class="add-item-input">
    <input type="text" v-model="newItem" />
    <button @click="addNewItem">Add</button>
  </div>
  <div v-show="!!totalTask">{{ totalDone + '/' + totalTask + ' task done.' }}</div>
  <List :listItem="listItem" :deleteItem="deleteItem" />
</template>

<script>
import List from './List.vue'

export default {
  name: 'ToDoList',
  data() {
    return {
      newItem: "",
      listItem: [],
    }
  },
  methods: {
    addNewItem() {
      console.log("newItem", this.newItem)
      if (!this.newItem) return;
      this.listItem.push({ text: this.newItem, checked: false })
      console.log("list Item", this.listItem)
      this.newItem = ''
    },
    deleteItem(index) {
      this.listItem.splice(index, 1)
    }
  },
  computed: {
    totalTask: function () {
      return this.listItem.length
    },
    totalDone: function () {
      return this.listItem.filter(item => item.checked === true).length
    }
  },
  components: {
    List
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.add-item-input {
  display: flex;
  justify-content: center;
}
</style>
