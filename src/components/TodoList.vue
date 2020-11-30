<template lang="pug">
  .container
    h1 Твой список дел <З    
    input(
      type='text' 
      placeholder="Что нужно?)"
      v-model.trim="newItem"
      @keyup.enter="addItem"
    )
    .todo__list-item(
      v-for="(item, index) in list"
      :name="item.name"
      :key="index"  
    )
      .todo__list-item-name(
        :class="{ complete: item.complete }"
        contenteditable="true"
        @keydown.enter="updateItem($event, item)"
        @blur="updateItem($event, item)"      
      ) {{ item.name }}
      button.todo__list-item-edit(        
        @click="completeItem(item)"        
      ) сделано
      button.todo__list-item-delete(
        @click="deleteItem($event, index)"
      ) удалить
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      list: []
    }
  },
  methods: {
    addItem() {
      if (this.newItem.length <= 0) {
        return false
      }
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
    updateItem(e, item) {
      item.name = e.target.innerText;
      e.target.blur();
    }
  },
}
</script>

<style lang="sass">
.container
  margin: 200px auto
  width: 500px
input
  width: 100%
.todo__list-item
  display: flex
  width: 100%
.todo__list-item-name
  margin-right: auto
  cursor: pointer
.complete 
  text-decoration: line-through
</style>