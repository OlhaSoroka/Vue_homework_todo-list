<template>
  <div
    class="text-center rounded-lg shadow-2xl p-4 w-80 text-teal-900 font-bold mx-4 h-5/6 flex flex-col justify-between mt-5">
    <div>
      <h2 class="uppercase mt-3">{{ list.name }}</h2>
      <ItemVue v-for="(item, index) in list.items" :key="index" :task="item" @toggleTask="onTaskToggle($event, index)"
        @deleteTask="onTaskDelete($event, index)" @editTask="onTaskEdit($event, index)">
      </ItemVue>
      <div v-if="list.items.length < 9"
        class=" bg-teal-700 h-12 rounded-md  flex justify-center items-center m-6 cursor-pointer">
        <button class="w-full h-full" @click="openModal"><span class="text-white uppercase font-bold">Add new
            task</span></button>
      </div>
    </div>
    <div>

      <button @click="deleteList" class="bg-red-500 text-white font-bold p-2 rounded-md w-full">Delete</button>
    </div>

    <div v-if="showModal"
      class="rounded-md p-6 shadow-2xl absolute w-1/3 h-48 bg-white border-2 border-teal-700 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 ">
      <h2 class="mb-2 text-center uppercase font-bold text-teal-700 ">Enter new task</h2>
      <input v-model="taskName" class="w-full mb-4 border-2 border-teal-700" type="text">
      <button @click="submitModal" class="bg-cyan-600 text-white font-bold p-2 rounded-md w-full">Submit</button>
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
  },
  data() {
    return {
      taskName: "",
      showModal: false,
    }
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    submitModal() {
      this.showModal = false;
      const newTask = {
        value: this.taskName,
        complete: false
      }
      this.$emit("createNewTask", newTask);
      this.taskName = "";
    },
    onTaskEdit(task, taskIndex) {
      this.$emit("taskEdit", { task: task, index: taskIndex })
    },
    onTaskDelete(task, taskIndex) {
      this.$emit("taskDelete", { task: task, index: taskIndex })
    },
    onTaskToggle(task, taskIndex) {
      this.$emit("taskToggle", { task: task, index: taskIndex })
    },
    deleteList() {
      this.$emit("deleteList")
    }
  }
}
</script>

