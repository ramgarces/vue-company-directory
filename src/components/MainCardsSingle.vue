<script setup>
import { ref } from 'vue'
import { faker } from '@faker-js/faker'

import useAPI from '@/composables/useAPI'
const { getDepartment } = useAPI()

const selectCard = () => {
  console.log(`${props.employee.name} selected`)
}

const props = defineProps({
  employee: {
    type: Object,
    required: true,
    default: () => {
      return {
        createdAt: '2022-01-01',
        departmentId: '123',
        email: 'john.doe@example.com',
        employeeId: '123',
        name: 'John Doe',
        quote: 'Really cool quote.',
        title: 'Position',
        updatedAt: '2022-01-01',
      }
    },
  },
})

const departmentResponse = await getDepartment(props.employee.departmentId)
const department = ref(departmentResponse)
</script>

<template>
  <div class="card" @click="selectCard">
    <div class="card-image">
      <img :src="faker.internet.avatar()" alt="" srcset="" />
    </div>
    <div class="card-details">
      <p class="card-details-name">{{ props.employee.name }}</p>
      <p class="card-details-job">{{ props.employee.title }}, {{ department.name }}</p>
      <p class="card-details-quote">"{{ props.employee.quote }}"</p>
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
    &-job {
      @apply -mt-2 text-sm  text-slate-700;
    }
    &-quote {
      @apply pt-4 text-lg italic text-slate-800;
    }
  }
}
</style>
