<template>
  <div class="bg-indigo-700 p-4">
<div class="min-h-screen p-20 bg-blue-400">
  <div class="bg-white p-4 rounded-lg">
    <div v-for="house in houses" :key="house.id" v-if="house.cover && house.cover.id">
      <img class="" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + '/small'"
           alt="cover">

      <div>{{ house.title }}</div>
      <div>{{ house.address }} {{ house.address2 }}</div>
      <button @click="singlePage(house)"
              :style="house.locked===1 ? 'background: grey; color: red' : 'background: grey; color: white'"
              :disabled="house.locked===1">Open
      </button>
    </div>
  </div>
</div>
  </div>
</template>

<script>
import axios from 'axios'



export default {

  data() {
    return {
      houses: []

    }
  },

  async mounted() {
    try {
      let res = await axios.get('http://homehapp-api.jsteam.gaussx.com/api/home?page=1&limit=10&sortBy=price&sortOrder=desc')
      this.houses = res.data.data.data
      console.log(this.houses)
    } catch (
      error
      ) {
      console.log(error)
    }
  },
  methods: {
    singlePage(house) {
      this.$router.push(`/about/${house.id}`)
    },

  }
}
</script>
<style>


</style>
