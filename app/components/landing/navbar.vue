<script setup lang="ts">
  import { Button } from "../ui/button"
  import { NavigationMenu, NavigationMenuList, NavigationMenuItem, NavigationMenuLink } from "../ui/navigation-menu"
</script>

<template>
  <nav class="bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
    <div class="container mx-auto px-7">
      <div class="flex h-16 items-center relative">
        <div class="flex items-center">
          <NuxtLink to="/" class="font-inspiration text-header-nav text-foreground hover:text-primary transition-colors">
            Jamee
          </NuxtLink>
        </div>

        <div class="hidden md:flex items-center space-x-8 absolute left-1/2 transform -translate-x-1/2">
          <NavigationMenu>
            <NavigationMenuList class="flex space-x-8">
              <NavigationMenuItem>
                <NuxtLink to="/">
                  <NavigationMenuLink class="text-black text-sm font-medium  hover:text-foreground transition-colors">
                    Preset/Design
                  </NavigationMenuLink>
                </NuxtLink>
              </NavigationMenuItem>
              <NavigationMenuItem>
                <NuxtLink to="/">
                  <NavigationMenuLink class="text-black text-sm font-medium hover:text-foreground transition-colors">
                    Portfolio
                  </NavigationMenuLink>
                </NuxtLink>
              </NavigationMenuItem>
              <NavigationMenuItem>
                <NuxtLink to="/">
                  <NavigationMenuLink class="text-black text-sm font-medium hover:text-foreground transition-colors">
                    Contact
                  </NavigationMenuLink>
                </NuxtLink>
              </NavigationMenuItem>
            </NavigationMenuList>
          </NavigationMenu>
        </div>

        <div class="hidden md:flex items-center space-x-3 ml-auto">
          <Button variant="outline" size="lg" class="rounded-full border-black">
            <NuxtLink to="/">
              Daftar
            </NuxtLink>
          </Button>
          <Button size="lg" class="rounded-full border-login border-1">
            <NuxtLink to="/">
              Masuk
            </NuxtLink>
          </Button>
        </div>

        <div class="md:hidden ml-auto">
          <Button class="text-muted-foreground hover:text-foreground">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
          </Button>
        </div>
      </div>
    </div>
  </nav>
</template>