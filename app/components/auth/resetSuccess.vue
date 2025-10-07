<script setup lang="ts">
  import { Button } from "@/components/ui/button"
  import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
</script>

<template>
  <main class="min-h-svh flex items-center justify-center p-6 bg-background text-foreground">
    <div class="w-full max-w-sm">
      <Card>
        <CardHeader>
          <div class="mx-auto mb-4 flex h-32 w-32 items-center justify-center rounded-full bg-orange-100 dark:bg-orange-900/20">
            <svg class="h-20 w-20 text-orange-600 dark:text-orange-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"></path>
            </svg>
          </div>
          <CardTitle class="text-balance text-center text-3xl">
            Password Diperbarui
          </CardTitle>
          <CardDescription class="text-pretty text-center text-base">
            Passwordmu telah berhasil diperbarui
          </CardDescription>
        </CardHeader>
        <CardContent>
          <Button class="w-full bg-black hover:bg-black/90 text-white dark:bg-white dark:text-black dark:hover:bg-white/90" as-child>
            <NuxtLink to="/login">
              Lanjutkan Login
            </NuxtLink>
          </Button>
        </CardContent>
      </Card>
    </div>
  </main>
</template>