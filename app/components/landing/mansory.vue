<script setup lang="ts">
  import { ref, onMounted } from "vue"
  import { Button } from "../ui/button"
  import { imageSlide } from "../../data/imageSlide"
  import { masonryLayout } from "../../data/masonryLayout"

  const isLoaded = ref(false)

  onMounted(() => {
    setTimeout(() => {
      isLoaded.value = true
    }, 100)
  })

  const mapImagesToLayout = () => {
    const images = imageSlide || []
    let imageIndex = 0
    
    return masonryLayout.map(column => column.map(slot => {
      const image = images[imageIndex % images.length]
      
      imageIndex++
      
      return {
        ...slot,
        image: image?.image || "/placeholder.svg",
        id: image?.id || imageIndex
      }
    }))
  }

  const layoutWithImages = mapImagesToLayout()
  
  const contentHeight = ref(0)
  onMounted(() => {
    const firstSetEl = document.querySelector(".first-set")
    if (firstSetEl) {
      contentHeight.value = firstSetEl.clientHeight
    }
  })
</script>

<template>
  <div class="bg-black text-white">
    <div class="flex h-screen max-h-[800px]">
      <div class="w-1/2 relative overflow-hidden p-6">
        <div class="relative h-full overflow-hidden group">
          <div :class="[{'animate-seamless-slow': isLoaded}, 'transition-all duration-1000 group-hover:[animation-play-state:paused]']">
            <div class="flex gap-3 first-set mb-3">
              <div v-for="(column, columnIndex) in layoutWithImages":key="`column-1-${columnIndex}`" class="flex flex-col gap-3 flex-1">
                <div v-for="(slot, slotIndex) in column" :key="`slot-1-${columnIndex}-${slotIndex}`" :class="`${slot.height} w-full rounded-lg overflow-hidden shadow-lg transition-all duration-700 hover:scale-105`">
                  <img :src="slot.image" :alt="`Wedding photo ${slot.id}`" class="w-full h-full object-cover"/>
                </div>
              </div>
            </div>
            
            <div class="flex gap-3 second-set">
              <div v-for="(column, columnIndex) in layoutWithImages" :key="`column-2-${columnIndex}`" class="flex flex-col gap-3 flex-1">
                <div v-for="(slot, slotIndex) in column" :key="`slot-2-${columnIndex}-${slotIndex}`" :class="`${slot.height} w-full rounded-lg overflow-hidden shadow-lg transition-all duration-700 hover:scale-105`">
                  <img :src="slot.image" :alt="`Wedding photo ${slot.id}`" class="w-full h-full object-cover"/>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="w-3/5 flex items-center justify-start pl-12 pr-8">
        <div class="max-w-xl">
          <h1 class="text-6xl font-bold text-yellow-400 mb-6 leading-tight">
            Wujudkan Impianmu
            <br />
            Bersama Pasangan
          </h1>

          <div class="text-yellow-600 text-2xl mb-8 font-medium">
            100.000 Kebahagiaan
          </div>

          <p class="text-gray-300 text-lg mb-10 leading-relaxed">
            Welcome to Burger Bliss, where we take your cravings to a whole new level! Our mouthwatering burgers are
            made from 100% beef and are served on freshly baked buns.
          </p>

          <div class="flex gap-6">
            <Button class="bg-yellow-500 hover:bg-yellow-600 text-black font-semibold px-8 py-4 rounded-full text-lg">
              Lihat Portfolio
            </Button>
            <Button variant="outline" class="border-yellow-500 text-yellow-500 hover:bg-yellow-500 hover:text-black font-semibold px-8 py-4 rounded-full text-lg bg-transparent">
              Buat Undanganmu Sekarang, Gratis!
            </Button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>