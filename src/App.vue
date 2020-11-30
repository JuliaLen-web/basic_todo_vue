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
      v-for="(item, i) in list"
      :name="item.name"
      :complete="item.complete"
      
    )
      .todo__list-item-name(
        :class="{ complete: item.complete }"
        contenteditable="true"
        @keydown.enter="updateItem($event, item)"
        @blur="updateItem($event, item)"      
      ) {{ item.name }}
      button.todo__list-item-edit(
        
        @click="completeItem($event, item)"
      ) сделано
      button.todo__list-item-delete(
        @click="deleteItem(i)"
      ) удалить
        
</template>

<script>
export default {
  name: "App",
  components: {
    
  },
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
    deleteItem(i) {
      this.list.splice(i, 1)
    },
    completeItem(item) {
      item.complete != item.complete
    },
    updateItem(e, item) {
      item.name = e.target.innerText
      e.target.blur()
    }
  },
  props: {
    name: String,
    complete: Boolean
  },
};
</script>

<style lang="sass">
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
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
