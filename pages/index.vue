<template>
  <div class="container mx-auto">
    <div class="house-container">

      <nuxt-link :to="'/about/' + house.id" v-for="house in houses" :key="house.id"class="block mb-8">
        <img :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + '/small'" alt="cover">
        <div>{{ house.title }}</div>
        <div>{{ house.address }} {{ house.address2 }}</div>
      </nuxt-link>
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
  }
}
</script>
<style>


</style>
