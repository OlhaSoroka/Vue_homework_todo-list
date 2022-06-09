<template>
  <div class="modal-window">
    <h2 class="modal-header">{{ header }}</h2>
    <input v-model="inputValue" class="modal-input" type="text">
    <button v-bind:class="{ 'disabled': inputValue.length < 3 || inputValue.length > 20 }" @click="submitModal"
      class="submit-btn">{{ buttonText
      }}</button>
  </div>
</template>

<script>
export default {
  props: {
    header: String,
    buttonText: String,
    defaultInputValue: {
      type: String,
      required: false,
      default: ""
    }
  },
  data() {
    return {
      inputValue: this.defaultInputValue
    }
  },
  methods: {
    submitModal() {
      this.$emit('onModalSubmit', this.inputValue)
      this.inputValue = ""
    }
  }
}
</script>

<style scoped>
.modal-window {

  @apply rounded-md p-6 shadow-2xl absolute w-1/4 h-48 bg-white border-2 border-teal-700 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2;

}

.modal-input {
  @apply w-full mb-4 border-2 rounded-md border-teal-700
}

.modal-header {
  @apply mb-2 text-center uppercase font-bold text-teal-700
}
</style>