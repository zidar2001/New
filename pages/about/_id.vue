<template>
  <div>
    <div class="bg-gray-600 ">
      <div class="container mx-auto flex items-end pb-8" style="height:350px">
        <div class="w-1/4"></div>
        <div class="w-1/2 ml-12">
          <h1 class="font-heading text-2xl text-white uppercase">{{ house.title }}</h1>
        </div>

      </div>
    </div>
    <div class="container mx-auto flex">
      <div class="w-1/4 -mt-16 ">
        <img class="rounded-md" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id " alt="cover"
             v-if="house.cover && house.cover.id">
        <div class="pt-3">
          <span class="font-bold">Adress:</span>
          <span>{{ house.address }} {{ house.address2 }}</span>
        </div>
      </div>
      <div class="w-3/5 ml-10 pt-6 space-y-1">
        <span class="font-bold "> Description: </span>
        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4 "
             v-html="house.description"></div>
        <span class="font-bold " v-if="house.hood && house.hood.text_lifestyle"> Lifestyle: </span>
        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4 "
             v-if="house.hood && house.hood.text_lifestyle">{{ house.hood.text_lifestyle }}
        </div>
        <span class="font-bold" v-if="house.hood && house.hood.text_neighbours"> Neighbours: </span>
        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4  "
             v-if="house.hood && house.hood.text_neighbours">{{ house.hood.text_neighbours }}
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
      house: {},
      isHydrated: false
    }
  },
  async mounted() {
    try {
      let res = await axios.get(`http://homehapp-api.jsteam.gaussx.com/api/home/${this.$route.params.id}`)
      console.log(res)
      this.house = res.data.data
      console.log(this.house)
      //this.isHydrated=true
    } catch (
      error
      ) {
      console.log(error)
    }
  }
}
</script>

