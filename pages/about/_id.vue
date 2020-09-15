<template>

  <div>
    <div class="font-bold uppercase m-6">{{ house.title }}</div>
    <div class="object-none object-center"> <img :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + '/small'" alt="cover"></div>

   <div class="text-center p-5 m-5 border-4 object-center" v-html="house.description"></div>

    <div class="font-bold ">{{ house.address }} {{ house.address2 }}</div>
    <div class="mt-1">
      {{house.price}}
      <span class="text-gray-600 text-sm">/ kn</span>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      house: []

    }
  },
  async mounted() {
    try {
      let res = await axios.get(`http://homehapp-api.jsteam.gaussx.com/api/home/${this.$route.params.id}`)
      this.house = res.data.data
      console.log(this.house)
    } catch (
      error
      ) {
      console.log(error)
    }
  }
}
</script>
