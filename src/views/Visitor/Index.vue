<template>
    <div class="flex flex-col lg:justify-between lg:flex-row-reverse">
        <div class="flex">
            <router-link to="/dashboard" class="capitalize text-blue-500">dashboard</router-link>/
            <router-link to="/pengunjung" class="capitalize text-blue-500">pengunjung</router-link>/
        </div>
        <div>
            <h1 class="capitalize text-2xl font-medium lg:text-3xl">pengunjung perpustakaan</h1>
            <p class="capitalize lg:text-lg">selamat datang di pengunjung perpustakaan</p>
        </div>
    </div>
    <div class="flex flex-col items-center">
        <div class="bg-blue-500 w-full h-44 rounded-3xl mt-8 shadow-sm flex flex-col gap-3 px-8 py-4 text-white -z-20">
            <div class="flex flex-col gap-3">
                <h6 class="capitalize lg:text-lg">total pengunjung perpustakaan</h6>
                <div class="text-6xl">
                    {{ count }}
                </div>
            </div>
        </div>
        <div ref="bookNav" class="bg-white w-4/5 h-20 rounded-3xl shadow-sm relative -top-10 flex flex-row items-center justify-evenly lg:justify-center lg:gap-3 z-0">
            <router-link to="/tambah-pengunjung" class="flex flex-col items-center lg:flex-row lg:gap-3 lg:bg-white lg:px-3 lg:py-2 lg:rounded-xl lg:shadow-customBoxShadow">
                <div class="bg-green-200 text-green-600 grid place-content-center text-2xl w-10 h-10 rounded-full"><i class="fa-solid fa-plus"></i></div>
                <small class="text-slate-600">Tambah Pengunjung</small>
            </router-link>
            <router-link to="/statistik-pengunjung" class="flex flex-col items-center lg:flex-row lg:gap-3 lg:bg-white lg:px-3 lg:py-2 lg:rounded-xl lg:shadow-customBoxShadow">
                <div class="bg-yellow-200 text-yellow-600 grid place-content-center text-2xl w-10 h-10 rounded-full"><i class="fa-solid fa-chart-simple"></i></div>
                <small class="text-slate-600 text-xs">Statistik</small>
            </router-link>
        </div>
        <div class="bg-white w-full h-12 rounded-xl overflow-hidden shadow-sm">
            <form class="flex items-center">
                <input type="text" placeholder="Cari Pengunjung Perpustakaan..." class="w-full h-12 px-6 text-lg outline-none" v-model="search">
            </form>
        </div>
        <div class="w-full grid grid-cols-1 gap-3 lg:grid-cols-2 mt-3">
            <div v-for="visitor in visitor" :key="visitor.id" class="bg-white w-full h-mx px-6 py-3 flex gap-3 rounded-3xl shadow-sm">
                <div class="flex flex-col lg:flex-row lg:justify-between gap-2 w-full">
                    <div class="flex flex-col gap-2">
                        <div class="w-full h-max">
                            <h5 class="font-medium">{{ visitor.name }}</h5>
                            <small class="xl:text-base capitalize">{{ visitor.role }}</small>
                        </div>
                        <div>
                            <p class="text-xs text-slate-600">{{ visitor.major.major }}</p>
                        </div>
                    </div>
                    <div class="flex flex-row gap-3 h-full ">
                        <router-link :to="'/edit-pengunjung/' + visitor.id" class="bg-blue-200 text-blue-600 px-3 py-2 rounded-lg h-max hover:bg-blue-100 hover:text-blue-500 hover:duration-150"><i class="fa-regular fa-pen-to-square"></i></router-link>
                        <form @submit.prevent="destroy(visitor.id)">
                            <button class="bg-red-200 text-red-600 px-3 py-2 rounded-lg hover:bg-red-100 hover:text-red-500 hover:duration-150"><i class="fa-solid fa-trash"></i></button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="flex justify-end mt-8">
    <div
      class="bg-white w-full lg:w-1/2 h-max p-3 rounded-full flex justify-between items-center"
    >
      <!-- Tombol Previous -->
      <div>
        <router-link
          :to="'' + (parseInt(route.params.page) - 1)"
          :class="{
            'text-blue-500': parseInt(route.params.page) > 1,
            'text-gray-500 pointer-events-none':
              parseInt(route.params.page) <= 1,
          }"
        >
          <i class="fa-solid fa-circle-chevron-left"></i>
        </router-link>
      </div>

      <!-- Pagination Links -->
      <div>
        <ul class="flex gap-4">
          <li v-for="page in totalPage" :key="page">
            <router-link
              :to="'' + page"
              :class="{
                'font-bold text-blue-500': parseInt(route.params.page) === page,
                'text-blue-500': parseInt(route.params.page) !== page,
              }"
            >
              {{ page }}
            </router-link>
          </li>
        </ul>
      </div>

      <!-- Tombol Next -->
      <div>
        <router-link
          :to="'' + (parseInt(route.params.page) + 1)"
          :class="{
            'text-blue-500': parseInt(route.params.page) < totalPage,
            'text-gray-500 pointer-events-none':
              parseInt(route.params.page) >= totalPage,
          }"
        >
          <i class="fa-solid fa-circle-chevron-right"></i>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, watch, ref } from 'vue'
import useVisitor from '../../service/data/visitor'
import { useRoute } from 'vue-router'

const route = useRoute()
const { visitor, getVisitor, destroy, totalPage, count } = useVisitor()
const search = ref('')


watch(
  () => route.params.page,
  () => {
    getVisitor(search.value)
  }
)

watch(search, (newSearch) => {
  getVisitor(newSearch)
});

onMounted(() => {
    getVisitor(search.value)
})
</script>