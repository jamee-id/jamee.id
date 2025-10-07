<script setup lang="ts">
  import { ref } from 'vue'
  import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'
  import { Button } from '@/components/ui/button'
  import { Label } from '@/components/ui/label'

  const newPassword = ref('')
  const confirmPassword = ref('')
  const passwordError = ref('')

  const isLoading = ref(false)

  const resetPassword = async () => {
    passwordError.value = ''
      
    if (newPassword.value !== confirmPassword.value) {
      passwordError.value = 'Kata sandi tidak cocok'
      return
    }
      
    if (newPassword.value.length < 8) {
      passwordError.value = 'Kata sandi minimal 8 karakter'
      return
    }
      
    isLoading.value = true
      
    await new Promise(resolve => setTimeout(resolve, 1000))
      
    console.log('Password reset successfully')
    isLoading.value = false
  }
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
            Buat Kata Sandi Baru
          </CardTitle>
          
          <CardDescription class="text-pretty text-center">
            Masukkan kata sandi baru Anda.
          </CardDescription>
        </CardHeader>
        
        <CardContent>
          <form @submit.prevent="resetPassword" class="grid gap-4">
            <div class="grid gap-2">
              <Label for="new-password">
                Kata Sandi Baru
              </Label>
              
              <Input id="new-password" v-model="newPassword" type="password" placeholder="••••••••" required minlength="8"/>
              
            </div>
            
            <div class="grid gap-2">
              <Label for="confirm-password">
                Konfirmasi Kata Sandi
              </Label>
              <Input id="confirm-password" v-model="confirmPassword" type="password" placeholder="••••••••" required minlength="8"/>
            </div>
              
            <p v-if="passwordError" class="text-sm text-destructive">
              {{ passwordError }}
            </p>
            <Button type="submit" class="w-full" :disabled="isLoading" as-child>
              <NuxtLink to="/reset-success">
                {{ isLoading ? 'Memperbarui...' : 'Perbarui Kata Sandi' }}
              </NuxtLink>
            </Button>
          </form>
        </CardContent>
      </Card>
    </div>
  </main>
</template>