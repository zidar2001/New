<template>
  <section class="w-full text-gray-700 body-font">
    <h1 class="text-2xl font-semibold uppercase text-center py-10">Nekretnine</h1>
    <div class="container px-6 mx-auto">
      <div class="flex flex-wrap -m-3">
        <div class="p-4 md:w-1/2 lg:w-1/3 sm:w-1/1 w-full" v-for="house in houses" :key="house.id"
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
                <div class="truncate">{{ house.address}} {{ house.address2}}</div>
                <div class="flex justify">
                  <div class="flex mx-2" >
                  <svg xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 24 24" height="24"
                       viewBox="0 0 24 24" width="24">
                    <g>
                      <rect fill="none" height="24" width="24"/>
                    </g>
                    <g>
                      <g>
                        <rect height="3" opacity=".3" width="12" x="6" y="12"/>
                        <path
                          d="M18,10V7c0-1.1-0.9-2-2-2H8C6.9,5,6,5.9,6,7v3c-1.1,0-2,0.9-2,2v5h1.33L6,19h1l0.67-2h8.67L17,19h1l0.67-2H20v-5 C20,10.9,19.1,10,18,10z M13,7h3v3h-3V7z M8,7h3v3H8V7z M18,15H6v-3h12V15z"/>
                      </g>
                    </g>
                  </svg>
                  <span>{{house.bedrooms}}</span>
                  </div>
                  <div class="flex justify">
                  <svg xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 24 24" viewBox="0 0 24 24"
                       fill="black" width="18px" height="18px">
                    <g>
                      <rect fill="none" height="24" width="24"/>
                    </g>
                    <g>
                      <g>
                        <rect height="4" opacity=".3" width="16" x="4" y="15"/>
                        <circle cx="7" cy="7" r="2"/>
                        <path
                          d="M20,13V4.83C20,3.27,18.73,2,17.17,2c-0.75,0-1.47,0.3-2,0.83l-1.25,1.25C13.76,4.03,13.59,4,13.41,4 c-0.4,0-0.77,0.12-1.08,0.32l2.76,2.76c0.2-0.31,0.32-0.68,0.32-1.08c0-0.18-0.03-0.34-0.07-0.51l1.25-1.25 C16.74,4.09,16.95,4,17.17,4C17.63,4,18,4.37,18,4.83V13h-6.85c-0.3-0.21-0.57-0.45-0.82-0.72l-1.4-1.55 c-0.19-0.21-0.43-0.38-0.69-0.5C7.93,10.08,7.59,10,7.24,10C6,10.01,5,11.01,5,12.25V13H2v6c0,1.1,0.9,2,2,2c0,0.55,0.45,1,1,1h14 c0.55,0,1-0.45,1-1c1.1,0,2-0.9,2-2v-6H20z M20,19H4v-4h16V19z"/>
                      </g>
                    </g>
                  </svg>
                  <span class="mx-1">{{ house.bathrooms }}</span>
                  </div>
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
    <pagination class="mt-4" :debounce="300" @input="setPage" :value="localPagination.page"
                :last-page="localPagination.lastPage"/>
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
      active: false,
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
