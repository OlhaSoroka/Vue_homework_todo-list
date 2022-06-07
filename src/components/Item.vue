<template>
  <div class="task-item">
    <div class="flex justify-between items-center">
      <div @click="toggleCheck" v-if="task.complete" class="task-checkbox-checked">
        <i class="fa-solid fa-check text-teal-700"></i>
      </div>
      <div @click="toggleCheck" v-else class="task-checkbox-unchecked"></div>
      <h2>{{ task.value }}</h2>
      <div class="flex justify-around items-center">
        <button @click="deleteTask"><i class="fa-solid fa-square-minus text-red-500 mr-2"></i></button>
        <button @click="openModal"><i class="fa-solid fa-pen-to-square text-teal-700"></i></button>
      </div>
    </div>
    <div v-if="showModal" class="modal-window">
      <h2 class="list-header">Edit task name</h2>
      <input v-model="editedTaskName" class="input-list-name" type="text">
      <button :class="{ 'disabled': editedTaskName.length < 3 }" @click="edit" class="submit-btn">Save</button>
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

<style scoped>
.task-item {
  @apply m-4 p-4 shadow-md border-2 border-teal-700 rounded-md
}

.task-checkbox-checked {
  @apply w-4 h-4 border-2 border-teal-700 flex justify-between items-center cursor-pointer
}

.task-checkbox-unchecked {
  @apply w-4 h-4 border-2 border-teal-700 cursor-pointer
}
</style>
