<script setup lang="ts">
  import { Badge } from "../ui/badge"
  import { Button } from "../ui/button"
  import IPhoneMockup from "./mockup.vue"
</script>

<template>
  <div class="min-h-screen bg-background">
    <!-- Hero Section -->
    <section class="relative overflow-hidden">
      <!-- Background Spotlight Effect -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute top-1/2 left-3/4 -translate-x-1/2 -translate-y-1/2 w-[500px] h-[500px] bg-[#FFB22C]/60 rounded-full blur-3xl"/>
      </div>
      
      <div class="container mx-auto px-4 py-16 lg:py-24 relative z-10">
        <div class="grid lg:grid-cols-2 gap-12 items-center">
          <!-- Left Content -->
          <div class="space-y-8">
            <div class="space-y-4">
              <Badge variant="secondary" class="text-sm font-medium">
                New Release
              </Badge>
              <h1 class="text-4xl lg:text-6xl font-black text-balance leading-tight">
                Lorem ipsum simply
                <span class="block text-primary">dummy</span>
              </h1>
              <p class="text-lg text-muted-foreground text-pretty max-w-md">
                Forged in titanium and featuring the groundbreaking A17 Pro chip, iPhone 15 Pro is a marvel of
                engineering that pushes the boundaries of what's possible.
              </p>
            </div>

            <div class="flex flex-col sm:flex-row gap-4">
              <Button size="lg" class="rounded-full border-login border-1 px-8">
                Order Now
              </Button>
              <Button variant="outline" size="lg" class="rounded-full border-black px-8">
                Explore
              </Button>
            </div>
          </div>

          <!-- Right Content - iPhone Mockup -->
          <div class="flex justify-center relative">
            <IPhoneMockup />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>