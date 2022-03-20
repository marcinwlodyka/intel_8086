<template>
  <div>
    <ul v-for="(item, i) in names" :key="i">
      <li class="flex flex-row ">
        <div class="flex m-1 items-center">
          <div class="w-10 text-center h-min">{{ item + 'H' }}</div>
          <input type="text">
        </div>
        <div class="flex m-1 items-center">
          <div class="w-10 text-center h-min">{{ item + 'L' }}</div>
          <input type="text">
        </div>
      </li>
    </ul>
    
    <button @click="test">test</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      names: [ 'A', 'B', 'C', 'D' ],
      inputs: [6]
    }
  },
  methods: {
    test() {
      this.inputs[1] = 10;
      console.log(this.inputs[1]);
    }
  }
}
</script>

<style scoped>
input {
  border: black solid 1px;
  border-radius: 1rem;
  padding: 0.25rem 1rem;
}
</style>