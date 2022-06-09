
<template>
  <div>
    <div class="main-header">
      todo list
    </div>
    <div class="flex relative">
      <ListVue v-for="(item, index) in board" @createNewTask="onTaskCreate($event, index)"
        @taskEdit="onTaskEdit($event, index)" @taskDelete="onTaskDelete($event, index)"
        @taskToggle="onTaskToggle($event, index)" @deleteList="onListDelete(index)" :key="index" :list="item">
      </ListVue>
      <div v-if="board.length < 5" class="add-btn">
        <button class="w-full h-full" @click="openModal"><span class="uppercase font-bold text-white">Add new
            list</span></button>
      </div>
      <ModalVue v-if="showModal" :header="'Enter new list name:'" :buttonText="'Create new list'"
        @onModalSubmit="submitModal($event)"></ModalVue>

    </div>
  </div>
</template>


<script>
import ListVue from './components/List.vue'
import ModalVue from './components/Modal.vue'
export default {
  components: {
    ListVue,
    ModalVue,


  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    submitModal(modalInputValue) {
      console.log(modalInputValue);
      const newList = {
        name: modalInputValue,
        items: []
      }
      this.board.push(newList);
      this.showModal = false;
    },
    onTaskCreate(newTask, listIndex) {
      this.board[listIndex].items.push(newTask);
    },
    onTaskEdit({ task, index }, listIndex) {
      this.board[listIndex].items[index] = task
    },
    onTaskDelete({ task, index }, listIndex) {
      this.board[listIndex].items.splice(index, 1)
    },
    onTaskToggle({ task, index }, listIndex) {
      this.board[listIndex].items[index] = task
    },
    onListDelete(listIndex) {
      this.board.splice(listIndex, 1)
    }

  },
  data() {
    return {

      showModal: false,
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
          ]
        },

      ]
    }
  }
}
</script>

<style>
.disabled {
  @apply opacity-50 pointer-events-none
}

.main-header {
  @apply font-bold text-3xl uppercase text-teal-700 border-4 border-teal-700 text-center w-1/3 mx-auto my-3 rounded-md
}

.add-btn {
  @apply w-48 bg-teal-700 h-48 rounded-md flex justify-center items-center m-6 cursor-pointer
}

.submit-btn {
  @apply bg-cyan-600 text-white font-bold p-2 rounded-md w-full
}
</style>

