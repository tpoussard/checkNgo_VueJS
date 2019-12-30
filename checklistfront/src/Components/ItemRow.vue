<template>
  <v-list-tile>
      <v-list-tile-content>
        <v-list-tile-title>{{ singleItem }}</v-list-tile-title>
      </v-list-tile-content>

      <v-list-tile-action>
        <v-checkbox
          :id='singleItem'
          v-model="selected"
          @change='checkingStatus(singleItem, itemsChecked)'
        ></v-checkbox>
      </v-list-tile-action>
  </v-list-tile>
</template>

<script>

export default {
  name: 'itemrow',
  props: ['singleItem', 'itemsChecked'],

  data: () => {
    return {
      selected: null
    }
  },

  // Loading checked items stored in localStorage
  mounted () {
    if (this.itemsChecked.includes(this.singleItem)) {
      this.selected = true
    }
  },

  methods: {
    // ADDing items in localstorage if checked, and removing them if unchecked
    checkingStatus: (itemName, listOfItemsChecked) => {
      if (listOfItemsChecked.includes(itemName)) {
        let index = listOfItemsChecked.indexOf(itemName)
        listOfItemsChecked.splice(index, 1) // delete 1 item on index 'index'
      } else {
        listOfItemsChecked.push(itemName)
      }

      localStorage.setItem('checkedItem-storage', JSON.stringify(listOfItemsChecked))
    }
  }
}
</script>

<style>

</style>
