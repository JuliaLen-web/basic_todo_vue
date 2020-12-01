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
      :item="item"
      @deleteItem="deleteItem($event, index)"
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