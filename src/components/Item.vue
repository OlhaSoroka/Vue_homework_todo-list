<template>
  <div class="m-4 p-4 shadow-md border-2 border-teal-700 rounded-md">
    <div class="flex justify-between items-center">
      <div @click="toggleCheck" v-if="checked"
        class="w-4 h-4 border-2 border-teal-700 flex justify-between items-center cursor-pointer">
        <i class="fa-solid fa-check text-teal-700"></i>
      </div>
      <div @click="toggleCheck" v-else class="w-4 h-4  border-2 border-teal-700 cursor-pointer"></div>
      <h2>{{ task.value }}</h2>
      <div class="flex justify-around items-center">
        <button><i class="fa-solid fa-square-minus text-red-500 mr-2"></i></button>
        <button><i class="fa-solid fa-pen-to-square text-teal-700"></i></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: Object,
  },
  data() {
    return {
      checked: false
    }
  },
  methods: {
    toggleCheck() {
      this.checked = !this.checked;
    }
  }

}
</script>

