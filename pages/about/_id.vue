<template>

  <div class="flex flex-wrap">
    <div class="text-center">
    <h1>  {{ house.title }} </h1>
    </div>
    <div class="w-full" style="text-align: center"><img class="mx-auto"
                                                        :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id + '/small'"
                                                        alt="cover" v-if="house.cover && house.cover.id"></div>


    <div class="w-full" v-html="house.description"></div>

    <div class="w-full">{{ house.address }} {{ house.address2 }}</div>
    <div class="w-full">
      {{ house.price }}
      <span class="">/ kn</span>
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

