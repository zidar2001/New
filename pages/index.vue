<template>
  <section class="text-gray-700 body-font">
    <h1 class="text-2xl font-semibold uppercase text-center py-10">Nekretnine</h1>
    <div class="container px-6 mx-auto">
      <div class="flex flex-wrap -m-4" >
        <div class="p-4 md:w-1/2 lg:w-1/3 sm:w-1/1" v-for="house in houses" :key="house.id" v-if="house.cover && house.cover.id" >
          <div class="h-full border-2 border-gray-200 rounded-lg overflow-hidden">
            <img class="h-48 w-full object-cover object-center" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id+'/small' " alt="cover">
            <div class="p-6">
              <h2 class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1" v-if="house.protected===1">Status: Protected</h2>
              <h2 class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1" v-else-if="house.protected===0">Status: Active</h2>
              <h1 class="title-font text-lg font-medium text-gray-900 mb-1 truncate uppercase">{{house.title}}</h1>
              <p class="leading-relaxed mb-3">{{house.address}} {{house.address2}}</p>

              <button class="bg-green-500 hover:bg-green-400 text-white font-bold py-1 px-5 border-b-2 border-green-700 hover:border-green-500 rounded-lg " v-if="house.locked===0" @click="singlePage(house)" >Open</button>
              <button class="border-double border-2 border-gray-600 px-5 py-1 rounded-lg bg-gray-400  " v-else-if="house.locked===1">Open</button>


<!--              <button class="px-4 py-1 rounded-lg " @click="singlePage(house)"
                      :style="house.locked===0 ?'background: #538d22; color: white' : 'background: grey;  color: red'" :disabled="house.locked===1" >Open</button>-->

            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<!--  <div class="container mx-auto py-16  ">
    <h1 class="text-2xl font-semibold uppercase mb-6 text-center">Nekretnine</h1>
    <div class="houses-container flex flex-wrap -mx-4 space-x-2 justify-center">
      <div v-for="house in houses" :key="house.id" v-if="house.cover && house.cover.id"
           class="w-full md:w-1/4 px-2 mb-12 sm:w-1/3 lg:w-1/5 no-underline h-full border-2 border-gray-400 rounded-lg overflow-hidden ">
        <img class=" object-cover h-48 w-full"
             :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + 'small'" alt="cover">
        <div class="text-black font-semibold text-lg truncate ...">
          {{ house.title }}
        </div>

        <div class="text-gray-700 truncate ...  pb-1">{{ house.address }} {{ house.address2 }}</div>
        <button class="px-4 py-1 rounded-lg " @click="singlePage(house)"
                :style="house.locked===1 ? 'background: grey; color: red' : 'background: #538d22;  color: white'"
                :disabled="house.locked===1">Open
        </button>
      </div>

    </div>
  </div>
</template>-->

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
