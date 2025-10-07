<script setup lang="ts">
  import { Input } from "@/components/ui/input"
  import { Button } from "@/components/ui/button"
  import { Checkbox } from "@/components/ui/checkbox"

  useHead({
    title: 'Jamee.Id | Masuk',
  })

  const isSubmitting = ref(false)
  const rememberMe = ref(false)

  async function onSubmit(e: Event) {
    e.preventDefault()
    const form = e.currentTarget as HTMLFormElement
    const formData = new FormData(form)
    const email = String(formData.get('email') || '')
    const password = String(formData.get('password') || '')

    try {
      isSubmitting.value = true
      console.log('[v0] Login attempt:', { email })
      await new Promise((r) => setTimeout(r, 600))
      console.log('[v0] Login success (simulasi)')
    } catch (err: any) {
      console.error('[v0] Login error:', err?.message || err)
    } finally {
      isSubmitting.value = false
    }
  }

  function handleGoogleLogin() {
    console.log('[v0] Google login clicked')
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
            Selamat Datang
          </h1>
          <p class="text-sm text-muted-foreground">
            Masukkan E-Mail dan kata sandi yang sudah terdaftar
          </p>
        </div>

        <form @submit="onSubmit" class="space-y-4">
          <Button type="button" variant="outline" class="w-full" @click="handleGoogleLogin">
            <span class="inline-flex items-center justify-center gap-2">
              <svg class="h-5 w-5" viewBox="0 0 24 24">
                <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
              </svg>
              <span>Continue with Google</span>
            </span>
          </Button>

          <!-- Divider -->
          <div class="relative">
            <div class="absolute inset-0 flex items-center">
              <span class="w-full border-t" />
            </div>
            <div class="relative flex justify-center text-xs uppercase">
              <span class="bg-background px-2 text-muted-foreground">
                or Sign In with Email
              </span>
            </div>
          </div>

          <!-- Email Field -->
          <div class="space-y-2">
            <label for="email" class="text-sm font-medium">
              Email
            </label>
            <Input id="email" name="email" type="email" inputmode="email" autocomplete="email" placeholder="example@mail.com" class="w-full" required/>
          </div>

          <!-- Password Field -->
          <div class="space-y-2">
            <label for="password" class="text-sm font-medium">
              Password
            </label>
            <Input id="password" name="password" type="password" placeholder="********" autocomplete="current-password" class="w-full" required/>
          </div>

          <!-- Remember Me & Forgot Password -->
          <div class="flex items-center justify-between">
            <div class="flex items-center space-x-2">
              <Checkbox id="remember" v-model:checked="rememberMe" />
              <label for="remember" class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70">
                Remember Me
              </label>
            </div>
            <NuxtLink to="/forgot-password" class="text-sm text-primary hover:underline">
              Lupa Password?
            </NuxtLink>
          </div>

          <!-- Login Button -->
          <Button type="submit" class="w-full" :disabled="isSubmitting">
            {{isSubmitting ? 'Memproses...' : 'Login' }}
          </Button>

          <!-- Sign Up Link -->
          <p class="text-center text-sm text-muted-foreground">
            Belum Punya Akun?
            <NuxtLink to="/register" class="text-foreground font-medium hover:underline">
              Buat Sekarang
            </NuxtLink>
          </p>
        </form>
      </div>
    </section>
  </main>
</template>