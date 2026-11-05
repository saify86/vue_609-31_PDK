<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

import ProductList from './components/ProductList.vue'

const items = ref([])

const fetchItems = async () => {
  try {
    const { data } = await axios.get(
      'https://be292e097ceb0b81.mokky.dev/items'
    )

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (e) {
    console.log(e)
  }
}

onMounted(async () => {
  await fetchItems()
})
</script>



<template>
  <div class="flex min-h-screen flex-col justify-between">
    <div class="mx-auto mb-25 w-full max-w-[1440px] px-6">
      <nav class="border-b border-slate-200 py-3">
        <div class="flex flex-wrap items-center justify-between gap-6">
          <div class="flex items-center gap-3">
            <img
              src="/logo.svg"
              alt="Behoof"
            />
            <p class="text-sm">
              Лучшие цены <br />
              в интернет-магазинах
            </p>
          </div>
          <ul class="flex flex-wrap gap-6">
            <li>
              <a href="#" class="flex items-center gap-3">
                <span
                  class="rounded-xl bg-slate-100 p-3.5 transition hover:bg-slate-200"
                >
                  <img src="/cart-icon.svg" alt="" />
                </span>
                Корзина
              </a>
            </li>
            <li>
              <a href="#" class="flex items-center gap-3">
                <span
                  class="rounded-xl bg-slate-100 p-3.5 transition hover:bg-slate-200"
                >
                  <img src="/like-outline.svg" alt="" />
                </span>
                Избранное
              </a>
            </li>
            <li>
              <a href="#" class="flex items-center gap-3">
                <span
                  class="rounded-xl bg-slate-100 p-3.5 transition hover:bg-slate-200"
                >
                  <img src="/orders-icon.svg" alt="" />
                </span>
                Заказы
              </a>
            </li>
          </ul>
        </div>
      </nav>
      <main class="pt-10">
        <h1 class="mb-5 text-[40px] font-bold">
          Каталог
        </h1>

        <product-list :items="items"></product-list>
      </main>
    </div>
    <footer class="bg-slate-100 p-6">
      <div class="text-center text-slate-500">
        Copyright © 2023 Behoof, Inc.
        Все права защищены
      </div>
    </footer>
  </div>
</template>

