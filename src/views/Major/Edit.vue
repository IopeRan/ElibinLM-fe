<template>
  <div class="flex flex-col lg:justify-between lg:flex-row-reverse">
    <div class="flex">
      <router-link to="/dashboard" class="capitalize text-blue-500"
        >dashboard</router-link
      >/
      <router-link to="/rak" class="capitalize text-blue-500"
        >jurusan</router-link
      >/
      <router-link to="/edit-jurusan" class="capitalize text-blue-500"
        >edit jurusan</router-link
      >/
    </div>
    <div>
      <h1 class="text-2xl font-medium lg:text-3xl">Edit Jurusan</h1>
      <p class="capitalize lg:text-lg">selamat datang di edit jurusan</p>
    </div>
  </div>
  <div class="bg-white w-full h-max my-8 rounded-3xl px-4 py-3 shadow-sm">
    <form @submit.prevent="doEdit()" class="capitalize flex flex-col gap-3 w-full lg:flex-row">
      <div class="flex flex-col gap-3 w-full">
        <div class="flex flex-col">
          <label for="major" class="font-medium text-slate-500">jurusan</label>
          <input
            type="text"
            class="text-black rounded-lg px-3 py-2 outline-none border border-slate-400"
            placeholder="Jurusan"
            id="major"
            required
            v-model="major.major"
          />
        </div>
        <div class="flex flex-row justify-between pb-8 capitalize">
          <router-link
            to="/jurusan/1"
            class="w-max h-max px-6 py-3 rounded-xl bg-red-500 text-white hover:bg-red-400 hover:duration-150"
            >batal</router-link
          >
          <button
            class="w-max h-max bg-green-500 text-white hover:bg-green-400 hover:duration-150 rounded-xl px-6 py-3"
          >
            Simpan
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import useMajor from '../../service/data/major'

const { major, show, edit } = useMajor()

onMounted(() => {
  show()
})

function doEdit() {
  edit(this.major)
}
</script>