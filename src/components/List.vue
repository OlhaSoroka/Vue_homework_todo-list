<template>
  <div class="list-item">
    <div>
      <h2 class="uppercase mt-3">{{ list.name }}</h2>
      <ItemVue v-for="(item, index) in list.items" :key="index" :task="item" @toggleTask="onTaskToggle($event, index)"
        @deleteTask="onTaskDelete($event, index)" @editTask="onTaskEdit($event, index)">
      </ItemVue>
      <div v-if="list.items.length < 9" class="add-list-btn">
        <button class="w-full h-full" @click="openModal"><span class="text-white uppercase font-bold">Add new
            task</span></button>
      </div>
    </div>
    <div>

      <button @click="deleteList" class="dlt-btn">Delete</button>
    </div>
    <ModalVue v-if="showModal" :header="'Enter new task:'" :buttonText="'Create new task'"
      @onModalSubmit="submitModal($event)"></ModalVue>
  </div>
</template>

<script>
import ItemVue from './Item.vue'
import ModalVue from './Modal.vue'
export default {
  components: {
    ItemVue,
    ModalVue,
  },
  props: {
    list: Object
  },
  data() {
    return {
      showModal: false,
    }
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    submitModal(modalInputValue) {
      this.showModal = false;
      const newTask = {
        value: modalInputValue,
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

<style scoped>
.list-item {
  @apply text-center rounded-lg shadow-2xl p-4 w-80 text-teal-900 font-bold mx-4 h-5/6 flex flex-col justify-between mt-5
}

.dlt-btn {
  @apply bg-red-500 text-white font-bold p-2 rounded-md w-full uppercase
}

.add-list-btn {
  @apply bg-teal-700 h-12 rounded-md flex justify-center items-center m-6 cursor-pointer
}
</style>

