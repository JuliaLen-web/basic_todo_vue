<template lang="pug"> 
  .todo__list-item
    input( 
      type="text"
      v-if="item === editingItem" 
      class="text-input" 
      @keyup.enter="$emit('editItem')" 
      @blur="$emit('editItem')" 
      v-model="name"
    )
    .todo__list-item-name(
      :class="{ 'complete': complete }" 
      v-if="item !== editingItem"
      @dblclick="$emit('editItem')"
    ) {{ name }}
    button.todo__list-item-edit(        
      @click="$emit('completeItem')"        
    ) сделано
    button.todo__list-item-delete(
      @click="$emit('deleteItem')"
    ) удалить
</template>

<script>
export default { 
  props: {
    item: Object,
    editingItem: Object,
    name: String,
    complete: Boolean
  },
  methods: {
    
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