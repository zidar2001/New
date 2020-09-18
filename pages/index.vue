<template>
  <section class="text-gray-700 body-font">
    <h1 class="text-2xl font-semibold uppercase text-center py-10">Nekretnine</h1>
    <div class="container px-6 mx-auto">
      <div class="flex flex-wrap -m-4">
        <div class="p-4 md:w-1/2 lg:w-1/3 sm:w-1/1" v-for="house in houses" :key="house.id"
             v-if="house.cover && house.cover.id">
          <div class="h-full border-2 border-gray-200 rounded-lg overflow-hidden">
            <img class="h-48 w-full object-cover object-center"
                 :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id+'/small' " alt="cover">
            <div class="p-6">
              <h2 class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1" v-if="house.protected===1">
                Status: Protected</h2>
              <h2 class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1"
                  v-else-if="house.protected===0">Status: Active</h2>
              <h1 class="title-font text-lg font-medium text-gray-900 mb-1 truncate uppercase">{{ house.title }}</h1>
              <div class="flex justify-between">

                  <p class="leading-relaxed mb-3">{{ house.address }} {{ house.address2 }} </p>
                  <div class="flex justify" >
                  <img class="w-4 h-5 mr-2" src="@/assets/css/icon1.png" alt="icon">
                    <span >{{house.bathrooms}}</span>
                    <img class="w-4 h-5" src="@/assets/css/icon1.png" alt="icon">
                </div>
              </div>
              <button
                class="bg-green-500 hover:bg-green-400 text-white font-bold py-1 px-5 border-b-2 border-green-700 hover:border-green-500 rounded-lg "
                v-if="house.locked===0" @click="singlePage(house)">Open
              </button>
              <button class="border-double border-2 border-gray-600 px-5 py-1 rounded-lg bg-gray-400  "
                      v-else-if="house.locked===1">Open
              </button>
            </div>
          </div>
        </div>
      </div>

    </div>
    <pagination :debounce="300" @input="setPage" :value="localPagination.page" :last-page="localPagination.lastPage"/>
  </section>
</template>

<script>
import axios from 'axios'
import pagination from "@/components/pagination";

export default {
  components: {
    pagination
  },
  data() {
    return {
      houses: [],
      localPagination: {
        page: 1,
      }
    }

  },

  async mounted() {
    this.getHouses()
  },

  methods: {
    singlePage(house) {
      this.$router.push(`/about/${house.id}`)
    },
    setPage(newPage) {
      this.localPagination.page = newPage
      this.getHouses()
    },
    async getHouses() {
      try {
        let res = await axios.get('http://homehapp-api.jsteam.gaussx.com/api/home?&limit=10&sortBy=price&sortOrder=desc', {
          params: {
            page: this.localPagination.page
          }
        })
        this.houses = res.data.data.data
        this.localPagination = res.data.data.pagination
        console.log(this.houses)
      } catch (
        error
        ) {
        console.log(error)
      }
    }
  }
}
</script>
<style>


</style>
