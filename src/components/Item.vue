<template>
  <div class="task-item">
    <div class="flex justify-between items-center">
      <div @click="toggleCheck" v-if="task.complete" class="task-checkbox-checked">
        <i class="fa-solid fa-check text-teal-700"></i>
      </div>
      <div @click="toggleCheck" v-else class="task-checkbox-unchecked"></div>
      <h2 class="task-name">{{ task.value }}</h2>
      <div class="flex justify-around items-center">
        <button @click="deleteTask"><i class="fa-solid fa-square-minus text-red-500 mr-2"></i></button>
        <button @click="openModal"><i class="fa-solid fa-pen-to-square text-teal-700"></i></button>
      </div>
    </div>
    <ModalVue v-if="showModal" :defaultInputValue="task.value" :header="'Edit task name:'" :buttonText="'Save'"
      @onModalSubmit="edit($event)">
    </ModalVue>
  </div>
</template>

<script>
import ModalVue from './Modal.vue'
export default {
  components: {
    ModalVue,
  },
  props: {
    task: Object,
  },
  data() {
    return {
      showModal: false,
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
    edit(modalInputValue) {
      const updatedTask = { value: modalInputValue, complete: this.task.complete };
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

.task-name {
  @apply overflow-hidden text-ellipsis whitespace-nowrap w-36
}
</style>


