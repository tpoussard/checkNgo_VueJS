<template>
  <v-layout row>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-toolbar color="blue" dark>
        <v-toolbar-title>Check&Go</v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>

          <v-list>
            <v-list-group
              v-for="category in filteredCategories"
              :key="category"
              no-action=""
            >

              <v-list-tile slot="activator">
                <v-list-tile-content>
                  <v-list-tile-title class="categoryTitle"> {{ category }} </v-list-tile-title>
                </v-list-tile-content>

                  <DisplayCount
                    :allItems="items"
                    :singleCategory='category'
                    :itemsChecked='checkedList'
                  ></DisplayCount>

              </v-list-tile>

            <Items
              :allItems="items"
              :singleCategory="category"
              :itemsChecked="checkedList"
            ></Items>

            </v-list-group>
          </v-list>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
// import axios from 'axios'
import ItemsList from './Items.vue'
import ItemsCounter from './ItemsCounter.vue'
const jsonData = require('../fr.json');

export default {
  name: 'category',

  components: {
    Items: ItemsList,
    DisplayCount: ItemsCounter
  },

  data: () => {
    return {
      items: [],
      checkedList: []
    }
  },

  mounted () {
    
    this.items = jsonData.categories
   // console.log('localeStorage', localeStorage)
   // console.log('localeStorage', localeStorage)
    
    
      /*
    // If no localstorage, fetch data with axios, create a localstorage, and store data
    if (!localStorage.getItem('item-storage')) {
      axios
        .get('http://checkngo.ighilr.fr/api/items/')
        .then(res => (this.items = res.data))
        .then(itemData => localStorage.setItem('item-storage', JSON.stringify(itemData)))
     localStorage.setItem('item-storage', JSON.stringify(this.items))
     console.log("localeStorage.getItem('item-storage')", localeStorage.getItem('item-storage'))
     localStorage.setItem('checkedItem-storage', JSON.stringify(this.checkedList))
    } else {
      // If a localStorage exist, fetch data directly in this Storage
      this.items = JSON.parse(localStorage.getItem('item-storage') || '[]')
      this.checkedList = JSON.parse(localStorage.getItem('checkedItem-storage') || '[]')
    }

*/
  },

  computed: {
    filteredCategories: function () {
      // return [...new Set(this.items.map(item => item.category_name))]
      return [...new Set(this.items.map(item => item.key))];

    }
  }
}
</script>

<style>

</style>
