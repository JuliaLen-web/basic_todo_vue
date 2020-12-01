<template lang="pug">
  .container
    h1 Твой список дел <З    
    input(
      type='text' 
      placeholder="Что нужно?)"
      v-model.trim="newItem"
      @keyup.enter="addItem"
    )
    TodoItem(
      v-for="(item, index) in list"      
      :key="index" 
      :item="list.item"
      :name="item.name"
      :complete="item.complete"
      @deleteItem="deleteItem($event, index)"
      @completeItem="completeItem(item)"
      @editItem="editItem(item)"
    )
</template>

<script>

import TodoItem from "./TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      newItem: '',
      editingItem: {},
      list: []
    }
  },
  methods: {
    addItem() {
      if(!this.newItem.length) return
      this.list.push({
        name: this.newItem, complete: false
      })
      this.newItem = ''
    },    
    deleteItem(e, index) {
      this.list.splice(index, 1)
    },
    completeItem(item) {
      item.complete = !item.complete;
    },
    editItem(item) {
      this.editingItem = item;
    }
  }
}
</script>

<style lang="sass">
.container
  margin: 200px auto
  width: 500px
input
  width: 100%

</style>