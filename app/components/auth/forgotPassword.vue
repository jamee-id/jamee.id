<script setup lang="ts">
  import { ref } from "vue"
  import { Label } from "@/components/ui/label"
  import { Input } from "@/components/ui/input"
  import { Button } from "@/components/ui/button"
  import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"

  const email = ref('')
  const isLoading = ref(false)
</script>

<template>
  <main class="min-h-svh flex items-center justify-center p-6 bg-background text-foreground">
    <div class="w-full max-w-sm">
      <Card>
        <div class="text-center">
          <NuxtLink to="/" class="font-inspiration text-header-nav text-foreground hover:text-primary transition-colors inline-block">
            Jamee
          </NuxtLink>
        </div>

        <CardHeader>
          <CardTitle class="text-balance text-center">
            Lupa Kata Sandi
          </CardTitle>

          <CardDescription class="text-pretty text-center">
            Masukkan alamat email Anda. Kami akan mengirim tautan untuk mengatur ulang kata sandi.
          </CardDescription>

        </CardHeader>

        <CardContent>
          <form @submit.prevent="" class="grid gap-4">
            <div class="grid gap-2">
              <Label for="email">
                Email
              </Label>

              <Input id="email" v-model="email" name="email" type="email" placeholder="nama@contoh.com" required/>
            
            </div>

            <Button type="submit" class="w-full" :disabled="isLoading" as-child>
              <NuxtLink to="/verify-otp">
                {{ isLoading ? 'Mengirim...' : 'Kirim Tautan Reset' }}
              </NuxtLink>
            </Button>
          </form>
        </CardContent>
      </Card>
    </div>
  </main>
</template>