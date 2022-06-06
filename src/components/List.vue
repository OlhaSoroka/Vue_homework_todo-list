<template>
  <div
    class="text-center rounded-lg shadow-2xl p-4 w-80 text-teal-900 font-bold mx-4 h-screen flex flex-col justify-between mt-5">
    <div>
      <h2 class="uppercase mt-3">{{ list.name }}</h2>
      <ItemVue v-for="(item, index) in list.items" :key="index" :task="item"></ItemVue>
      <div
        class="w-auto bg-teal-700 h-12 rounded-md uppercase text-white flex justify-center items-center font-bold m-6 cursor-pointer">
        <div><span>Add new task</span></div>
      </div>
    </div>
    <div>

      <button class="bg-red-500 text-white font-bold p-2 rounded-md w-full">Delete</button>
    </div>
  </div>
</template>

<script>
import ItemVue from './Item.vue'
export default {
  components: {
    ItemVue
  },
  props: {
    list: Object
  }
}
</script>

