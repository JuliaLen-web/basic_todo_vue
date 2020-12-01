<template lang="pug"> 
  .todo__list-item
    input( 
      type="text"
      v-if="item === editingItem" 
      @keyup.enter="endEdit(item)" 
      @blur="endEdit(item)" 
      v-model="item.name"
    )
    .todo__list-item-name(
      :class="{ 'complete': item.complete }" 
      v-if="item !== editingItem"
      @dblclick="editItem(item)"
    ) {{ item.name }}
    button.todo__list-item-edit(        
      @click="switchCompletion(item)"        
    ) сделано
    button.todo__list-item-delete(
      @click="$emit('deleteItem')"
    ) удалить
</template>

<script>
export default { 
  props: {
    item: Object
  },
  data() {
    return {
      editingItem: {}
    }
  },
  methods: {
    switchCompletion(item) {
      item.complete = !item.complete;
    },
    editItem(item) {
      this.editingItem = item;
    },
    endEdit(item) {
      this.editItem = {};
      if (item.name.trim() === ""){
        this.$emit('deleteItem');
      }
    }
  }
}
</script>

<style lang="sass">
.todo__list-item
  display: flex
  width: 100%
.todo__list-item-name
  margin-right: auto
  cursor: pointer
.complete 
  text-decoration: line-through
</style>