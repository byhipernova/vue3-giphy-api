
<script setup>
import Preview from '@/components/Preview.vue'
</script>
<template>
  <div>
    <header>
      <input type="text" placeholder="Search..." v-model="query" @keyup.enter="searchHandle">
    </header>
    <main>
      <Preview v-for="gif in gifs" :key="gif.id" :data="gif" />
    </main>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      gifs: [],
      query: ""
    }
  },
  created() {
    axios
      .get('https://api.giphy.com/v1/gifs/trending?api_key=lRWM1bfyIkOdzxCdoaZ0z9ZQ2c0aL0Li&limit=24')
      .then((response) => {
        this.gifs = response.data.data
      })
  },
  methods: {
    searchHandle() {
      if (this.query == "") {
        axios
          .get('https://api.giphy.com/v1/gifs/trending?api_key=lRWM1bfyIkOdzxCdoaZ0z9ZQ2c0aL0Li&limit=24')
          .then((response) => {
            this.gifs = response.data.data
          })
      } else {
        axios
          .get('https://api.giphy.com/v1/gifs/search?api_key=lRWM1bfyIkOdzxCdoaZ0z9ZQ2c0aL0Li&limit=24&q=' + this.query)
          .then((response) => {
            this.gifs = response.data.data
          })
      }

    }
  }
}
</script>

<style lang="scss">
header {
  display: flex;
  justify-content: center;
  align-items: center;

  input {
    border-radius: 1.5rem;
    padding: .5rem 1rem;
    width: 100%;
    max-width: 400px;
  }
}

main {
  display: flex;
  flex-wrap: wrap;
  padding: 1rem;
}
</style>
