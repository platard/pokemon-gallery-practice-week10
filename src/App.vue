<template>
  <div class="gallery-title">
    <h1>Pokemon Gallery</h1>
    <form @submit.prevent="addItem">
      <input v-model="newItem.name" type="text" placeholder="Name">
      <button type="submit">Add Item</button>
    </form>
  </div>
  <Gallery :items="items" @toggle-caught="updateCaughtStatus"/> 
</template>

<script>
import Gallery from "./components/Gallery.vue"
import pokedex from "./utils/pokedex"

export default {
  components: {Gallery},
  // Component configuration
  data: function() {
        return {
          items: pokedex,
          newItem: {
              id: null,
              name: '',
              caught: false
          }
        }
    },

  methods: {
    updateCaughtStatus(updatedItem) {
      // const index = this.items.findIndex(item => item.id === updatedItem.id);
      // this.items[index].caught = !this.items[index].caught
      this.items = this.items.map(item => item.id === updatedItem.id ? {...item, caught: !item.caught} : item)

    },
    addItem() { 
      const newId = this.items.length +1
      this.newItem.id = newId
      this.items.push(this.newItem)

      this.newItem = {
            id: null,
            name: '',
            caught: false
            }
    } 
  },

  watch: {
    items: {
      handler: function(newItems) {
        localStorage.setItem('items', JSON.stringify(newItems));
      },
      deep: true
    },
},
created() {
  const storedItems = localStorage.getItem('items');
  if (storedItems) {
  this.items = JSON.parse(storedItems);
  }
}
}
</script>