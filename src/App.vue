
<template>
  <div class="flex relative">
    <ListVue v-for="(item, index) in board" :key="index" :list="item"></ListVue>
    <div
      class="w-48 bg-teal-700 h-48 rounded-md uppercase text-white flex justify-center items-center font-bold m-6 cursor-pointer">
      <div><span>Add new list</span></div>
    </div>
    <div
      class="rounded-md p-6 shadow-2xl absolute w-1/3 h-48 bg-white border-2 border-teal-700 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 ">
      <h2 class="mb-2 text-center uppercase font-bold text-teal-700">Enter list name please</h2>
      <input class="w-full mb-4 border-2 border-teal-700" type="text">
      <button class="bg-cyan-600 text-white font-bold p-2 rounded-md w-full">Submit</button>
    </div>
  </div>
</template>


<script>
import ListVue from './components/List.vue'
export default {
  components: {
    ListVue
  },
  data() {
    return {
      board: [
        {
          name: "First list",
          items: [
            {
              value: "Go to gym ",
              complete: false,
            },
            {
              value: "Driver classes",
              complete: true,
            },
            {
              value: "English lessons",
              complete: true,
            },
            {
              value: "Work meeting",
              complete: true,
            },
            {
              value: "Go to gym ",
              complete: false,
            },
            {
              value: "Driver classes",
              complete: true,
            },
            {
              value: "English lessons",
              complete: true,
            },
            {
              value: "Work meeting",
              complete: true,
            },
            {
              value: "Go to gym ",
              complete: false,
            },
            {
              value: "Driver classes",
              complete: true,
            },
            {
              value: "English lessons",
              complete: true,
            },
            {
              value: "Work meeting",
              complete: true,
            },
            {
              value: "Work meeting",
              complete: true,
            },

          ]
        },
        {
          name: "Second list",
          items: [
            {
              value: "Find a job",
              complete: true,
            }

          ]
        }
      ]
    }
  }
}
</script>

<style>
</style>
