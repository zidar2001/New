<template>
  <div>
    <navigation/>
    <nuxt/>
  </div>
</template>


<script>
import Navigation from "@/components/navigation";
export default {
  components: {
    Navigation
  }
}
</script>
<style>
textarea:focus, button:focus{
  outline: none;
}
</style>
