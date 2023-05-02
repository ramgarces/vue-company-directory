<script setup>
import useAPI from '@/composables/useAPI'

const { activePage, pages, getEmployees } = useAPI()

const prevPage = async () => {
  if (activePage.value > 1) {
    activePage.value--
    await getEmployees()
  }
}

const nextPage = async () => {
  if (activePage.value < pages.value) {
    activePage.value++
    await getEmployees()
  }
}

const jumpPage = async (page) => {
  activePage.value = page
  await getEmployees()
}
</script>

<template>
  <div class="pagination">
    <button class="action" :disabled="activePage === 1" @click="prevPage">Prev</button>
    <button
      v-for="page in pages"
      :key="page"
      class="page"
      :class="page === activePage ? 'active' : ''"
      @click="jumpPage(page)"
    >
      {{ page }}
    </button>
    <button class="action" :disabled="activePage === pages" @click="nextPage">Next</button>
  </div>
</template>

<style scoped lang="postcss">
.pagination {
  @apply flex justify-center gap-4;
  .action {
    @apply rounded-md bg-green-800 p-2 font-medium text-neutral-200 shadow-md
    hover:bg-green-600 disabled:text-green-500 hover:disabled:bg-green-200;
  }
  .page {
    @apply rounded-md bg-green-800 p-2 font-medium text-slate-200 shadow-md
    hover:bg-green-600;
    &.active {
      @apply bg-green-500 text-slate-100 hover:bg-green-400;
    }
  }
}
</style>
