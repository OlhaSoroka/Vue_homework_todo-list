
<template>
  <div>
    <div class="main-header">
      todo
      list
    </div>
    <div class="flex relative">
      <ListVue v-for="(item, index) in board" @createNewTask="onTaskCreate($event, index)"
        @taskEdit="onTaskEdit($event, index)" @taskDelete="onTaskDelete($event, index)"
        @taskToggle="onTaskToggle($event, index)" @deleteList="onListDelete(index)" :key="index" :list="item">
      </ListVue>
      <div v-if="board.length < 5" class="add-btn">
        <button class="w-full h-full" @click="openModal"><span class="uppercase font-bold text-white ">Add new
            list</span></button>
      </div>
      <div v-if="showModal" class="modal-window">
        <h2 class="list-header">Enter list name please</h2>
        <input v-model="listName" class="input-list-name" type="text">
        <button :class="{ 'disabled': listName.length < 3 }" @click="submitModal" class="submit-btn">Create new
          list</button>
      </div>
    </div>
  </div>
</template>


<script>
import ListVue from './components/List.vue'
export default {
  components: {
    ListVue
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    submitModal() {
      console.log(this.listName);
      const newList = {
        name: this.listName,
        items: []
      }
      this.board.push(newList);
      this.showModal = false;
      this.listName = "";
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
      listName: "",
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

.modal-window {
  @apply rounded-md p-6 shadow-2xl absolute w-1/4 h-48 bg-white border-2 border-teal-700 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2;
}

.main-header {
  @apply font-bold text-3xl uppercase text-teal-700 border-4 border-teal-700 text-center w-1/3 mx-auto my-3 rounded-md
}

.add-btn {
  @apply w-48 bg-teal-700 h-48 rounded-md flex justify-center items-center m-6 cursor-pointer
}

.list-header {
  @apply mb-2 text-center uppercase font-bold text-teal-700
}

.input-list-name {
  @apply w-full mb-4 border-2 rounded-md border-teal-700
}

.submit-btn {
  @apply bg-cyan-600 text-white font-bold p-2 rounded-md w-full
}
</style>
