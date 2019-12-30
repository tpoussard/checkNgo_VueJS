<template>
  <div>
    <div
      v-for="item in filteredItems"
      :key="item.id"
      >
        <itemrow
          :singleItem="item.name"
          :itemsChecked="itemsChecked"
        ></itemrow>
    </div>
  </div>
</template>

<script>

import itemrow from './ItemRow'

export default {
  name: 'items',
  props: ['singleCategory', 'allItems', 'itemsChecked'],
  components: {
    itemrow: itemrow
  },

  computed: {
    filteredItems: function () {
      const singleCategory = this.singleCategory
      return this.allItems.filter(function (item) {
        return (item.category_name === singleCategory)
      })
    }
  }
}
</script>

<style>

</style>
