<template>
  <div class="flex flex-row items-center text-center bg-black rounded-full wrapper">
    <label for="name" class="capitalize mr-1 ml-3 text-white">{{ name }}</label>
    <select 
      :name="name" 
      :id="name"
      class="uppercase"
      @input="$emit('input', $event.target.value)"
    >
      <option  
        v-for="(option, i) in options"
        :key="i"
        :value="i"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    options: Array
  }
}
</script>

</script>

<style scoped>
select {
  background-color: white;
  border: black solid 2px;
  border-radius: 10rem;
  padding: 0.25rem 1rem;
}
.wrapper {
  width: min-content;
  height: min-content;
}
</style>