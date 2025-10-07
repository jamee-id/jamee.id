<script setup lang="ts">
  //
</script>

<template>
  <div class="relative">
    <!-- Frame -->
    <div class="relative w-[240px] h-[500px] bg-gradient-to-b from-gray-800 to-gray-900 rounded-[48px] p-2 shadow-2xl">
      <!-- Inner frame -->
      <div class="w-full h-full bg-black rounded-[40px] p-1">
        <!-- Screen -->
        <div class="w-full h-full bg-white rounded-[36px] overflow-hidden relative">
          <!-- Dynamic Island -->
          <div class="absolute top-4 left-1/2 -translate-x-1/2 w-24 h-6 bg-black rounded-full z-10"/>

          <!-- Screen Content - Sample Image -->
          <div class="w-full h-full flex items-center justify-center bg-gradient-to-br from-blue-500 via-purple-500 to-pink-500"/>
            <!-- <img
              src="/modern-abstract-wallpaper-with-vibrant-colors-and-.jpg"
              class="w-full h-full object-cover"
            > -->
          <!-- </div> -->

          <!-- Home indicator -->
          <div class="absolute bottom-2 left-1/2 -translate-x-1/2 w-24 h-1 bg-black/30 rounded-full"/>
        </div>
      </div>

      <!-- Side buttons -->
      <div class="absolute -left-[2px] top-[90px] w-1 h-10 bg-gray-700 rounded-l-sm"/>
      <div class="absolute -left-[2px] top-[120px] w-1 h-12 bg-gray-700 rounded-l-sm"/>
      <div class="absolute -left-[2px] top-[150px] w-1 h-12 bg-gray-700 rounded-l-sm"/>
      <div class="absolute -right-[2px] top-[135px] w-1 h-16 bg-gray-700 rounded-r-sm"/>
    </div>

    <!-- Floating elements for visual appeal -->
    <!-- <div class="absolute -top-3 -right-3 w-6 h-6 bg-primary/20 rounded-full animate-pulse"/> -->
    <div class="absolute -bottom-6 -left-6 w-8 h-8 bg-accent/20 rounded-full animate-pulse delay-1000"/>
  </div>
</template>