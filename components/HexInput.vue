<template>
  <div class="flex flex-row bg-black rounded-full items-center wrapper">
    <span class="text-white mr-1 ml-3">{{ name }}</span>
    <input type="text" @input="sendHex($event.target.value)" class="border-2 border-black rounded-full uppercase" maxlength="8">
  </div>
</template>

<script>
export default {
  props: {
    name: String
  },
  data: () => ({
    hexDigits: [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'a', 'b', 'c', 'd', 'e', 'f' ],
    firstDigit: '0',
    secondDigit: '0'
  }),
  methods: {
    sendHex(hex) {
      this.$emit('send', hex);
    }
  }
}
</script>

<style scoped>
input {
  background-color: white;
  padding: 0.25rem 1rem;
}
.wrapper {
  width: min-content;
  height: min-content;
}
</style>