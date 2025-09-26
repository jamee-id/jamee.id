<script setup lang="ts">
  import { Button } from "../ui/button"
  import { imageSlide, type ImageSlide } from '../../data/imageSlide'
  import { ref, onMounted } from 'vue'

  // Untuk memastikan animasi dimulai setelah komponen dirender
  const isLoaded = ref(false)
  onMounted(() => {
    setTimeout(() => {
      isLoaded.value = true
    }, 100)
  })

  const getPhotoSize = (size: ImageSlide['size']): string => {
    switch (size) {
      case 'large':
        return 'h-64'
      case 'medium':
        return 'h-48'
      case 'small':
        return 'h-32'
      default:
        return 'h-48'
    }
  }

  // Memvariasikan ukuran gambar untuk transisi yang lebih mulus
  const getVariedPhotoSize = (originalSize: ImageSlide['size'], position: 'top' | 'middle' | 'bottom', setIndex: number): string => {
    // Variasi hanya untuk posisi transisi (atas set kedua & bawah set pertama)
    
    // Set 1 bagian bawah - Variasi pada bagian bawah set pertama
    if (position === 'bottom' && setIndex === 1) {
      switch (originalSize) {
        case 'large': return 'h-60' // Sedikit lebih kecil dari aslinya
        case 'medium': return 'h-52' // Sedikit lebih besar dari aslinya
        case 'small': return 'h-36' // Sedikit lebih besar dari aslinya
        default: return 'h-48'
      }
    } 
    // Set 2 bagian atas - Variasi pada bagian atas set kedua
    else if (position === 'top' && setIndex === 2) {
      switch (originalSize) {
        case 'large': return 'h-68' // Berbeda dari bawah set pertama
        case 'medium': return 'h-44' // Berbeda dari bawah set pertama
        case 'small': return 'h-38' // Berbeda dari bawah set pertama
        default: return 'h-48'
      }
    }
    
    // Gambar lainnya tetap dengan ukuran asli
    return getPhotoSize(originalSize)
  }

  // Function to create a more intelligent masonry layout that fills gaps
  const createMasonryColumns = (images: ImageSlide[], numColumns: number = 3) => {
    // Bagi gambar ke dalam kolom secara seimbang
    const columns: ImageSlide[][] = Array.from({ length: numColumns }, () => [])
    
    // Helper untuk menghitung tinggi berdasarkan ukuran
    const getHeightValue = (size: ImageSlide['size']): number => {
      switch (size) {
        case 'large': return 64 // h-64 = 256px
        case 'medium': return 48 // h-48 = 192px
        case 'small': return 32 // h-32 = 128px
        default: return 48
      }
    }
    
    // Track tinggi setiap kolom untuk distribusi yang lebih baik
    const columnHeights = Array(numColumns).fill(0)
    
    // Distribusikan gambar berdasarkan tinggi kolom terpendek
    if (images && images.length) {
      // Urutkan gambar dari besar ke kecil
      const sortedImages = [...images].sort((a, b) => {
        const aValue = getHeightValue(a.size)
        const bValue = getHeightValue(b.size)
        return bValue - aValue // Urutkan dari besar ke kecil
      })
      
      // Distribusikan gambar ke kolom terpendek
      sortedImages.forEach((image) => {
        // Temukan kolom dengan tinggi terpendek
        const shortestColumnIndex = columnHeights.indexOf(Math.min(...columnHeights))
        
        // Tambahkan gambar ke kolom terpendek
        if (!columns[shortestColumnIndex]) columns[shortestColumnIndex] = []
        columns[shortestColumnIndex].push(image)
        
        // Update tinggi kolom (+3 untuk gap)
        columnHeights[shortestColumnIndex] += getHeightValue(image.size) + 12 // gap 3rem
      })
    }
    
    return { columns, columnHeights }
  }

  // Buat dua set kolom untuk efek seamless scroll
  // Set pertama untuk ditampilkan di awal, set kedua untuk duplikat di bawah
  const { columns: firstSetColumns, columnHeights: firstSetHeights } = createMasonryColumns(imageSlide || [])
  
  // Gunakan salinan yang sama untuk set kedua
  const secondSetColumns = [...firstSetColumns]
  
  // Hitung banyaknya gambar di setiap kolom untuk variasi nanti
  const columnImageCounts = firstSetColumns.map(col => col.length)
  
  // Untuk mengidentifikasi posisi gambar (atas/tengah/bawah) dalam setiap kolom
  const getImagePosition = (colIndex: number, imgIndex: number, setIndex: number): 'top' | 'middle' | 'bottom' => {
    // Pastikan colIndex valid
    if (colIndex < 0 || colIndex >= columnImageCounts.length) {
      return 'middle'
    }
    
    const totalInColumn = columnImageCounts[colIndex] ?? 0
    
    // Jika kolom kosong atau indeks tidak valid
    if (totalInColumn === 0 || imgIndex < 0 || imgIndex >= totalInColumn) {
      return 'middle'
    }
    
    // Tetapkan posisi gambar berdasarkan indeksnya dalam kolom
    if (imgIndex === 0) return 'top'
    if (imgIndex === totalInColumn - 1) return 'bottom'
    
    // Jika kolom memiliki 3+ gambar, gambar tengah tetap 'middle'
    return 'middle'
  }
  
  // Tinggi total konten untuk animasi seamless scroll yang tepat
  const contentHeight = ref(0)
  onMounted(() => {
    // Hitung tinggi total konten untuk animasi scroll yang benar
    const firstSetEl = document.querySelector('.first-set')
    if (firstSetEl) {
      contentHeight.value = firstSetEl.clientHeight
    }
  })
</script>

<template>
  <div class="bg-black text-white">
    <div class="flex h-screen max-h-[800px]">
      <!-- Left side with masonry grid -->
      <div class="w-2/5 relative overflow-hidden p-6">
        <div class="relative h-full overflow-hidden">
          <!-- Wrapper dengan tinggi tetap untuk seamless scroll -->
          <div 
            :class="[
              {'animate-seamless-slow': isLoaded}, 
              'transition-all duration-1000'
            ]"
          >
            <!-- First set of images -->
            <div class="flex gap-3 first-set mb-3">
              <div
                v-for="(column, columnIndex) in firstSetColumns"
                :key="`column-1-${columnIndex}`"
                class="flex flex-col gap-3 flex-1"
              >
                <div
                  v-for="(photo, photoIndex) in column"
                  :key="`${photo.id}-${photoIndex}-${columnIndex}-1`"
                  :class="`${getVariedPhotoSize(photo.size, getImagePosition(columnIndex, photoIndex, 1), 1)} w-full rounded-lg overflow-hidden shadow-lg transition-all duration-700 hover:scale-105`"
                >
                  <img
                    :src="photo.image || '/placeholder.svg'"
                    :alt="`Wedding photo ${photo.id}`"
                    class="w-full h-full object-cover"
                  />
                </div>
              </div>
            </div>
            
            <!-- Second set of images (duplicate for seamless loop) -->
            <div class="flex gap-3 second-set">
              <div
                v-for="(column, columnIndex) in secondSetColumns"
                :key="`column-2-${columnIndex}`"
                class="flex flex-col gap-3 flex-1"
              >
                <div
                  v-for="(photo, photoIndex) in column"
                  :key="`${photo.id}-${photoIndex}-${columnIndex}-2`"
                  :class="`${getVariedPhotoSize(photo.size, getImagePosition(columnIndex, photoIndex, 2), 2)} w-full rounded-lg overflow-hidden shadow-lg transition-all duration-700 hover:scale-105`"
                >
                  <img
                    :src="photo.image || '/placeholder.svg'"
                    :alt="`Wedding photo ${photo.id}`"
                    class="w-full h-full object-cover"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right side content -->
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

    <div class="bg-gray-900 p-8">
      <div class="text-center text-gray-400">
        <p>
          Additional content can go here...
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Tambahan style untuk animasi scroll yang lebih mulus */
@keyframes gradual-scroll {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(calc(-50% - 0.75rem)); /* -50% - gap untuk menyesuaikan */
  }
}

.animate-seamless-slow {
  animation: gradual-scroll 40s linear infinite;
}

.animate-seamless-slow:hover {
  animation-play-state: paused;
}
</style>