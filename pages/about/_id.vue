<template>
  <div>
  <navigation/>
<!--  <div>-->
<!--    <div class="bg-gray-600 ">-->
<!--      <div class="container mx-auto flex items-end pb-8" style="height:350px">-->
<!--        <div class="w-1/4"></div>-->
<!--        <div class="w-1/2 ml-12">-->
<!--          <h1 class="font-heading text-2xl text-white uppercase">{{ house.title }}</h1>-->
<!--        </div>-->

<!--      </div>-->
<!--    </div>-->
<!--    <div class="container mx-auto flex">-->
<!--      <div class="w-1/4 -mt-16 ">-->
<!--        <img class="rounded-md" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id " alt="cover"-->
<!--             v-if="house.cover && house.cover.id">-->
<!--        <div class="pt-3">-->
<!--          <span class="font-bold">Address:</span>-->
<!--          <span>{{ house.address }} {{ house.address2 }}</span>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="w-3/5 ml-10 pt-6 space-y-1">-->
<!--        <span class="font-bold "> Description: </span>-->
<!--        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4 "-->
<!--             v-html="house.description"></div>-->
<!--        <span class="font-bold " v-if="house.hood && house.hood.text_lifestyle"> Lifestyle: </span>-->
<!--        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4 "-->
<!--             v-if="house.hood && house.hood.text_lifestyle">{{ house.hood.text_lifestyle }}-->
<!--        </div>-->
<!--        <span class="font-bold" v-if="house.hood && house.hood.text_neighbours"> Neighbours: </span>-->
<!--        <div class="w-3/3 ml-12 pt-3 pb-3 text-justify border-2 border-gray-600 rounded-md px-4  "-->
<!--             v-if="house.hood && house.hood.text_neighbours">{{ house.hood.text_neighbours }}-->
<!--        </div>-->

<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
  <div>
    <div class="backBtn">
    <button class="btnBack" @click=" $router.back()">back</button>
    </div>
    <div class="background">
      <div class="container " style="height:300px">
        <div class="width1"></div>
        <div class="width2">
          <h1 class="heading">{{ house.title }}</h1>
        </div>

      </div>
    </div>
    <div class="container2">
      <div class="img ">
        <img class="img_dec" :src="'http://homehapp-api.jsteam.gaussx.com/api/media/' + house.cover.id " alt="cover"
             v-if="house.cover && house.cover.id">
        <div class="img_text">
          <span style="font-weight: bold">Adress:</span>
          <span>{{ house.address }} {{ house.address2 }}</span>
        </div>
      </div>
      <div class="des">
        <span style="font-weight: bold"> Description: </span>
        <div v-if="house.description" class="description "
             v-html="house.description"></div>
        <span style="font-weight: bold" v-if="house.hood && house.hood.text_lifestyle"> Lifestyle: </span>
        <div class="description"
             v-if="house.hood && house.hood.text_lifestyle">{{ house.hood.text_lifestyle }}
        </div>
        <span style="font-weight: bold" v-if="house.hood && house.hood.text_neighbours"> Neighbours: </span>
        <div class="description "
             v-if="house.hood && house.hood.text_neighbours">{{ house.hood.text_neighbours }}
        </div>

      </div>
    </div>
  </div>
  </div>
</template>
<script>
import axios from 'axios'
import Navigation from "@/components/navigation";

export default {
  components: {Navigation},
  data() {
    return {
      house: {},
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
<style>
.background{
  background: lightgray;
}
.container{
  width: 100%;
  margin: auto;
  display: flex;
}
.width1{
  width: 25%;
}
.width2{
  width: 50%;
  margin-left: 6rem;
}
.heading{
  padding-top: 16rem;
  font-size: 1.5rem;
  color: #fff;
  text-transform: uppercase;
}
.container2{
 width: 85%;
  margin-left: auto;
  margin-right: auto;
}
.img{
  width: 25%;
  margin-top: -3rem;
}
.img_dec{
  border-radius: 0.375rem;
}
.img_text{
  padding-top: 14px;
}
.des{
  width: 60%;
  margin-left: 23.5rem;
  margin-top: -8rem;
}
.description{
  width: 100%;
  margin-left: 3rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  text-align: justify;
  border-width: 2px;
  border-color: #718096;
  border-radius: 0.375rem;
  padding-left: 1rem;
  padding-right: 1rem;
}
.backBtn{
  background: lightgray;
padding-left: 9.30rem;
  padding-top: 1rem;
}
.btnBack{
  border-width: 2px;
  border-radius: 0.375rem;
  border-color: #38a169;
  padding-top: 2px;
  padding-bottom: 2px;
  padding-left: 4px;
  padding-right: 4px;
}
</style>
