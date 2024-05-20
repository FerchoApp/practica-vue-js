<script setup>
import { ref } from "vue"

const items = ref([
  { title: "Tema 1", subtitle: "Texto del tema 1", estado: false },
  { title: "Tema 2", subtitle: "Texto del tema 2", estado: false },
  { title: "Tema 3", subtitle: "Texto del tema 3", estado: false },
  { title: "Tema 4", subtitle: "Texto del tema 4", estado: false },
  { title: "Tema 5", subtitle: "Texto del tema 5", estado: false },
  { title: "Tema 6", subtitle: "Texto del tema 6", estado: false },
  
]);

const gridLayout = ref('grid-cols-3');

function mostrar(index) {
  items.value[index].estado = !items.value[index].estado;
  for (let i = 0; i < items.value.length; i++) {
    if (i !== index) {
      items.value[i].estado = false;
    }
  }
}

function Filas() {
  gridLayout.value = 'grid-rows-3';
}

function Columnas() {
  gridLayout.value = 'grid-cols-3';
}
</script>
<template>
  <div class="container mx-auto p-4 pt-12">
    <div class="flex flex-wrap justify-start mb-4">
      <button class="mr-2 rounded bg-slate-600 h-10 w-10" @click="Filas">F</button>
      <button class="mr-2 rounded bg-slate-500 h-10 w-10" @click="Columnas">C</button>
    </div>

    <div :class="gridLayout" class="bg-slate-400 grid gap-4 rounded  w-[600px] ">
      <div class="w-full sm:w-1/2 md:w-1/3 p-4" v-for="(item, i) in items" :key="i">
        <div class="flex h-20 w-[150px] bg-white shadow-md rounded-lg px-4 py-6">
          <div class="flex justify-between items-center py-2">
            <h3 class="text-lg font-bold">{{ item.title }}</h3>
            <span class="text-2xl cursor-pointer" @click="mostrar(i)">
                {{ item.estado ? '-' : '+' }}
            </span>
            </div>
            <div v-show="item.estado" class="bg-gray-100 p-4 mt-4">
                {{ item.subtitle }}
            </div>
        </div>
      </div>
    </div>
  </div>
</template>