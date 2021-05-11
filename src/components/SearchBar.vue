<template>
  <input type="text" :value="inputText" @keyup.enter="inputChange">
</template>

<script>
export default {
  name: 'SearchBar',
  props: {
    inputText: {
      type: String
    }
  },
  methods: {
    inputChange(event) {
      // console.log(event.target.value)
      this.$emit('input-change', event.target.value)
    }
  }
}
</script>

<style scoped>
input {
  width: 80%;
  height: 30px;
  font-size: 20px;
}
</style>
