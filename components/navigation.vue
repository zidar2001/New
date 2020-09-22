<template>
  <header class="text-gray-700 body-font sm:rounded-t text-blue-600 font-semibold  py-3 px-4 border-2 border-blue-200 rounded">
    <div class="container mx-auto justify-items-center flex flex-wrap p-5 flex-col md:flex-row items-center ">
      <nuxt-link to="/" class="flex title-font font-medium items-center text-gray-900 mb-4 sm:text-xs md:mb-0 inline-block">
        <svg stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
             class="w-10 h-10 p-2  bg-green-600 rounded-full" viewBox="0 0 24 24">
          <path
            d="M 12 3 L 2 12 h 3 v 8 h 6 v -6 h 2 v 6 h 6 v -8 h 3 L 12 3 Z m 5 15 h -2 v -6 H 9 v 6 H 7 v -7.81 l 5 -4.5 l 5 4.5 V 18 Z"></path>
        </svg>
      </nuxt-link>
      <nuxt-link to="/" class="mt-1">
        <span class="m-2">Home</span>
      </nuxt-link>


      <nav class="md:ml-auto md:mr-auto flex flex-wrap items-center text-base justify-center">
        <nuxt-link to="" class="mr-5 hover:text-gray-900">SELL & LET</nuxt-link>
        <nuxt-link to="" class="mr-5 hover:text-gray-900">BUY & RENT</nuxt-link>
        <nuxt-link to="" class="mr-5 hover:text-gray-900">SHOWCASES</nuxt-link>
        <nuxt-link to="" class="mr-5 hover:text-gray-900">AGENTS</nuxt-link>
        <nuxt-link to="" class="hover:text-gray-900">NEIGHBOURHOODS</nuxt-link>


      </nav>
      <span>
        <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0V0z"
                                                                                                 fill="none"/><path
          d="M12 6c1.1 0 2 .9 2 2s-.9 2-2 2-2-.9-2-2 .9-2 2-2m0 9c2.7 0 5.8 1.29 6 2v1H6v-.99c.2-.72 3.3-2.01 6-2.01m0-11C9.79 4 8 5.79 8 8s1.79 4 4 4 4-1.79 4-4-1.79-4-4-4zm0 9c-2.67 0-8 1.34-8 4v3h16v-3c0-2.66-5.33-4-8-4z"/></svg>
      </span>
      <nuxt-link to=""
        class="inline-flex items-center bg-gray-200 border-0 py-1 px-3 focus:outline-none hover:bg-gray-300 rounded text-base sm:text-xs mt-4 md:mt-0">
        Sign in

      </nuxt-link>
    </div>
  </header>
</template>
