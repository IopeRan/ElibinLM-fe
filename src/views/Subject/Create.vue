<template>
    <div class="flex flex-col lg:justify-between lg:flex-row-reverse">
      <div class="flex">
        <router-link to="/dashboard" class="capitalize text-blue-500"
          >dashboard</router-link
        >/
        <router-link to="/subjek/1" class="capitalize text-blue-500">subjek</router-link>/
        <router-link to="/tambah-subjek" class="capitalize text-blue-500"
          >tambah rak</router-link
        >/
      </div>
      <div>
        <h1 class="text-2xl font-medium lg:text-3xl">Tambah Subjek</h1>
        <p class="capitalize lg:text-lg">selamat datang di tambah subjek</p>
      </div>
    </div>
    <div class="bg-white w-full h-max my-8 rounded-3xl px-4 py-3 shadow-sm">
      <form @submit.prevent="doCreate()" class="capitalize flex flex-col gap-3 w-full lg:flex-row">
        <div class="flex flex-col gap-3 w-full">
          <div class="flex flex-col">
            <label for="subject" class="font-medium text-slate-500">subjek</label>
            <input
              type="text"
              class="text-black rounded-lg px-3 py-2 outline-none border border-slate-400"
              placeholder="Subjek"
              id="subject"
              required
              v-model="forms.subject"
            />
          </div>
          <div class="flex flex-row justify-between pb-8 capitalize">
            <router-link
              to="/rak/1"
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
  import { reactive } from 'vue'
  import useSubject from '../../service/data/subject'
  
  const { create } = useSubject()
  
  const forms = reactive({
    subject: ''
  })
  
  function doCreate() {
    create({...forms})
  }
  </script>