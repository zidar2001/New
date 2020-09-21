<template>
  <div>
    <div class="hero bg-gray-600 ">
      <div class="container mx-auto flex items-end pb-8" style="height:350px">
        <div class="w-1/4"></div>
        <div class="w-3/4 ml-12">
          <h1 class="font-heading text-white uppercase">{{ house.title }}</h1>

        </div>
      </div>
    </div>
    <div class="container mx-auto flex">
      <div class="w-1/4 -mt-16 max-w-sm rounded overflow-hidden shadow-lg">
        <img :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id " alt="cover" v-if="house.cover && house.cover.id">
      </div>
      <div class="w-3/4 ml-12">
      </div>
    </div>
  </div>
</template>


<!--  <div class=" flex content-center">-->
<!--    <div>-->
<!--      <div class="content-center">-->
<!--    <h1 > {{ house.title }} </h1>-->
<!--      </div>-->
<!--    </div>-->
<!--    <div class="w-full" style=""><img class="" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + '/small'"-->
<!--                                                        alt="cover" v-if="house.cover && house.cover.id"></div>-->


<!--    <div class="w-full" v-html="house.description"></div>-->

<!--    <div class="w-full">{{ house.address }} {{ house.address2 }}</div>-->
<!--    <div class="w-full">-->
<!--      {{ house.price }}-->
<!--      <span class="">/ kn</span>-->
<!--    </div>-->

<!--  </div>-->


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

