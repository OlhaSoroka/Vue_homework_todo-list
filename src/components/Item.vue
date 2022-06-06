<template>
  <div class="m-4 p-4 shadow-md border-2 border-teal-700 rounded-md">
    <div class="flex justify-between items-center">
      <div @click="toggleCheck" v-if="task.complete"
        class="w-4 h-4 border-2 border-teal-700 flex justify-between items-center cursor-pointer">
        <i class="fa-solid fa-check text-teal-700"></i>
      </div>
      <div @click="toggleCheck" v-else class="w-4 h-4  border-2 border-teal-700 cursor-pointer"></div>
      <h2>{{ task.value }}</h2>
      <div class="flex justify-around items-center">
        <button @click="deleteTask"><i class="fa-solid fa-square-minus text-red-500 mr-2"></i></button>
        <button @click="openModal"><i class="fa-solid fa-pen-to-square text-teal-700"></i></button>
      </div>
    </div>
    <div v-if="showModal"
      class="rounded-md p-6 shadow-2xl absolute w-1/3 h-48 bg-white border-2 border-teal-700 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 ">
      <h2 class="mb-2 text-center uppercase font-bold text-teal-700 ">Edit task name</h2>
      <input v-model="editedTaskName" class="w-full mb-4 border-2 border-teal-700" type="text">
      <button @click="edit" class="bg-cyan-600 text-white font-bold p-2 rounded-md w-full">Save</button>
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
      showModal: false,
      editedTaskName: this.task.value,
    }
  },
  methods: {
    toggleCheck() {
      const updatedTask = { value: this.task.value, complete: !this.task.complete };
      this.$emit("toggleTask", updatedTask)
    },
    deleteTask() {
      this.$emit("deleteTask", this.task)
    },
    edit() {
      const updatedTask = { value: this.editedTaskName, complete: this.task.complete };
      this.$emit("editTask", updatedTask);
      this.showModal = false;
    },
    openModal() {
      this.showModal = true;
    }
  }

}
</script>

