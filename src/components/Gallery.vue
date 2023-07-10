<template>
    <div id="gallery" class="gallery">
        <div v-for="item in items" :key="item.id" class="gallery-item" @click="toggleCaught(item)" 
        :class="item.caught ? 'gallery-item caught' : 'gallery-item'">
            <img class="gallery-item-image" :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${item.id}.png`" :alt="item.name" />
            <h2 class="gallery-item-name">{{ item.name }}</h2>
        </div>
    </div>
</template>

<script>
  export default {
    name: "Gallery",
    props: ['items'],
    methods: {
        toggleCaught: function(item) {
            this.$emit('toggle-caught', item)
            console.log(item.name)
        }
        }

  }
</script>