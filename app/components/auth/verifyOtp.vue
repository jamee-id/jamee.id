<script setup lang="ts">
  import { ref, onMounted, onUnmounted } from "vue"
  import { Button } from "@/components/ui/button"
  import { PinInput, PinInputGroup, PinInputSlot } from "@/components/ui/pin-input"
  import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"

  const email = ref('example@email.com')
  const otpCode = ref([])
  
  const isLoading = ref(false)
  const timer = ref(30)
  let timerInterval: ReturnType<typeof setInterval> | null = null
  
  const startTimer = () => {
    if (timerInterval) {
      clearInterval(timerInterval)
    }
    
    timerInterval = setInterval(() => {
      if (timer.value > 0) {
        timer.value--
      } else {
        if (timerInterval) {
          clearInterval(timerInterval)
        }
      }
    }, 1000)
  }
  
  onMounted(() => {
    startTimer()
  })
  
  onUnmounted(() => {
    if (timerInterval) {
      clearInterval(timerInterval)
    }
  })

  const handleSubmit = () => {
    console.log('OTP Code:', otpCode.value)
  }

  const handleResend = () => {
    console.log('Resend OTP')
    otpCode.value = []
    timer.value = 30
    startTimer()
  }
</script>

<template>
  <main class="min-h-svh flex items-center justify-center p-6 bg-background text-foreground">
    <div class="w-full max-w-sm">
      <Card>
        <CardHeader>
          <CardTitle class="text-balance text-center">
            Verifikasi Kode
          </CardTitle>
          <CardDescription class="text-pretty text-center">
            Masukkan kode OTP 6 digit yang kami kirim ke {{ email }}.
          </CardDescription>
        </CardHeader>
        <CardContent>
          <form @submit.prevent="handleSubmit" class="grid gap-4">
            <div class="grid gap-2">
              <div class="flex justify-center">
                <PinInput id="pin-input" v-model="otpCode" placeholder="○" :otp="true">
                  <PinInputGroup class="gap-3">
                    <PinInputSlot v-for="(id, index) in 4" :key="id" :index="index" class="h-16 w-16 rounded-lg border-2 text-2xl font-semibold"/>
                  </PinInputGroup>
                </PinInput>
              </div>
              <div class="text-center mt-3">
                <span class="text-sm text-red-500 font-medium">
                  {{ String(Math.floor(timer / 60)).padStart(2, '0') }}:{{ String(timer % 60).padStart(2, '0') }}
                </span>
              </div>
            </div>
            <Button type="submit" class="w-full" :disabled="isLoading || otpCode.length !== 4" as-child>
              <NuxtLink to="/reset-password">
                {{ isLoading ? 'Memverifikasi...' : 'Verifikasi' }}
              </NuxtLink>
            </Button>
          </form>
          <p class="mt-4 text-sm text-muted-foreground text-center">
            Tidak menerima kode?
            <Button variant="ghost" @click="handleResend" class="underline underline-offset-4 hover:text-foreground transition-colors">
              Kirim ulang
            </Button>
          </p>
        </CardContent>
      </Card>
    </div>
  </main>
</template>