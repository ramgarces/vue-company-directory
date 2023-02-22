<script setup>
import { ref } from 'vue'
import { useAuth } from '@/composables/useAuth'

const { isAuthenticated, logout, user } = useAuth()

const brand = ref(import.meta.env.VITE_APP_NAME)
</script>

<template>
  <nav>
    <div class="wrapper">
      <RouterLink :to="{ name: 'Home' }" class="brand">
        <span class="brand-title">{{ brand }}</span>
      </RouterLink>
      <div class="menu">
        <p v-show="isAuthenticated" class="px-2 py-4">
          Welcome back
          <strong class="text-green-800"
            ><i>{{ user.name }}</i></strong
          >
        </p>
        <div v-if="isAuthenticated">
          <RouterLink :to="{ name: 'Settings' }" class="menu-item">Settings</RouterLink>
          <button :to="{ name: 'Home' }" class="menu-logout" @click="logout">Logout</button>
        </div>
        <div v-else>
          <RouterLink :to="{ name: 'Login' }" class="menu-login">Login</RouterLink>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped lang="postcss">
nav {
  @apply flex h-20 bg-neutral-900 px-6 text-slate-200;
  .wrapper {
    @apply container mx-auto flex w-full items-center justify-between;
    .brand {
      &-title {
        @apply text-2xl font-bold text-slate-100;
      }
    }
    .menu {
      @apply flex gap-2;
      & div {
        @apply py-2;
      }
      &-item {
        @apply rounded-md px-4 py-2 hover:bg-green-800 hover:text-slate-900;
      }
      &-login {
        @apply rounded-md bg-green-800 px-4 py-2 hover:bg-green-700
        hover:text-slate-100;
      }
      &-logout {
        @apply mx-2 rounded-md bg-neutral-500 px-4 py-2 hover:bg-red-700
        hover:text-slate-100;
      }
    }
  }
}
</style>
