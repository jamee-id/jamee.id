<script setup lang="ts">
  import { Input } from "@/components/ui/input"
  import { Button } from "@/components/ui/button"
  import { Checkbox } from "@/components/ui/checkbox"

  useHead({
    title: 'Jamee.Id | Masuk',
  })

  const isSubmitting = ref(false)
  const rememberMe = ref(false)

  function handleGoogleLogin() {
    console.log('[v0] Google login clicked')
  }

  const formData = ref({
    name: '',
    email: '',
    password: ''
  })

  const onSubmit = () => {
    console.log('Register submitted', formData.value)
  }
</script>

<template>
  <main class="min-h-screen grid grid-cols-1 md:grid-cols-2">
    <aside class="relative hidden md:block">
      <img src="/wedding-1.jpg" alt="Ilustrasi ruang kerja modern" class="absolute inset-0 h-full w-full object-cover">
    </aside>

    <section class="flex items-center justify-center p-6 md:p-10 bg-background">
      <div class="w-full max-w-md">
        <div class="text-center">
          <NuxtLink to="/" class="font-inspiration text-header-nav text-foreground hover:text-primary transition-colors inline-block">
            Jamee
          </NuxtLink>
        </div>

        <div class="mb-6 text-center">
          <h1 class="text-2xl font-bold mb-2">
            Buat Akunmu
          </h1>
          <p class="text-sm text-muted-foreground">
            Daftar dan mulai buat undangan pernikahan digitalmu
          </p>
        </div>

        <form @submit="onSubmit" class="space-y-4">

          <!-- Email Field -->
          <div class="space-y-2">
            <label for="email" class="text-sm font-medium">
              Email
            </label>
            <Input id="email" name="email" type="email" inputmode="email" autocomplete="email" placeholder="example@mail.com" class="w-full" required/>
          </div>

          <!-- Username Field -->
          <div class="space-y-2">
            <label for="username" class="text-sm font-medium">
              Username
            </label>
            <Input id="username" name="username" type="text" inputmode="text" autocomplete="username" placeholder="your_username" class="w-full" required/>
          </div>

          <!-- Password Field -->
          <div class="space-y-2">
            <label for="password" class="text-sm font-medium">
              Password
            </label>
            <Input id="password" name="password" type="password" placeholder="********" autocomplete="current-password" class="w-full" required/>
          </div>

          <!-- Confirm Password Field -->
          <div class="space-y-2">
            <label for="confirm-password" class="text-sm font-medium">
              Confirm Password
            </label>
            <Input id="confirm-password" name="confirm-password" type="password" placeholder="********" autocomplete="current-password" class="w-full" required/>
          </div>

          <!-- Login Button -->
          <Button type="submit" class="w-full" :disabled="isSubmitting">
            {{isSubmitting ? 'Memproses...' : 'Register' }}
          </Button>

          <!-- Sign Up Link -->
          <p class="text-center text-sm text-muted-foreground">
            Sudah Punya Akun?
            <NuxtLink to="/login" class="text-foreground font-medium hover:underline">
              Masuk Sekarang
            </NuxtLink>
          </p>
        </form>
      </div>
    </section>
  </main>
</template>