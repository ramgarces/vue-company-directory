<script setup>
import { faker } from '@faker-js/faker'

const firstName = faker.name.firstName()
const lastName = faker.name.lastName()
const fullName = `${firstName} ${lastName}`

const selectCard = () => {
  console.log(`${firstName} ${lastName}`)
}
</script>

<template>
  <div class="card" @click="selectCard">
    <div class="card-image">
      <img :src="faker.internet.avatar()" alt="" srcset="" />
    </div>
    <div class="card-details">
      <p class="card-details-name">{{ fullName }}</p>
      <p class="card-details-email">{{ faker.internet.exampleEmail(firstName, lastName) }}</p>
      <p class="card-details-quote">"{{ faker.lorem.paragraph() }}"</p>
    </div>
  </div>
</template>

<style scoped lang="postcss">
.card {
  @apply cursor-pointer overflow-hidden rounded-md bg-slate-100 p-8 shadow-md
  transition-transform duration-300 hover:scale-105 hover:shadow-xl
  hover:shadow-green-900;
  &-image {
    img {
      @apply mx-auto rounded-lg object-contain;
    }
  }
  &-details {
    @apply flex flex-col gap-2 pt-6 text-center;
    &-name {
      @apply text-3xl font-thin tracking-wider text-green-800;
    }
    &-email {
      @apply -mt-2 text-sm  text-slate-700;
    }
    &-quote {
      @apply pt-4 text-lg italic text-slate-800;
    }
  }
}
</style>
