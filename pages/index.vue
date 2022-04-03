<template>
  <div class="h-screen">
    <form 
      @submit.prevent=""
      class="flex flex-row items-center w-1/2 h-1/2"
    >
      <ul class="flex flex-row flex-wrap">
        <li 
          v-for="(register, i) in registers"
          :key="i"
          class="w-1/2 my-2 flex flex-row justify-center"
        >
          <div class="bg-black p-0.5 rounded-full flex flex-row items-center">
            <label 
            :for="register.name"
            class="uppercase mx-2 text-white"
          >
            {{ register.name }}
          </label>
          <input 
            type="text"
            :name="register.name"
            :id="register.name"
            maxlength="2"
            autocomplete="off"
            v-model="register.value"
          >
          </div>
        </li>
      </ul>

      <div class="flex flex-col px-10">
        <input
          type="submit"
          value="Save"
          class="cursor-pointer"
        >
        <button>Reset</button>
        <button>Random</button>
      </div>
    </form>    
  </div>
</template>

<script>
export default {
  data() {
    return {
      registers: [
        {
          name: 'ah',
          value: ''
        },
        {
          name: 'al',
          value: ''
        },
        {
          name: 'bh',
          value: ''
        },
        {
          name: 'bl',
          value: ''
        },
        {
          name: 'ch',
          value: ''
        },
        {
          name: 'cl',
          value: ''
        },
        {
          name: 'dh',
          value: ''
        },
        {
          name: 'dl',
          value: ''
        }
      ]
    }
  },
  methods: {
    
  }
}
</script>

<style scoped>
input,
button {
  background-color: white;
  border: black solid 1px;
  border-radius: 1rem;
  padding: 0.25rem 1rem;
}

input[type = "submit"],
button {
  margin: 0.25rem auto;
  width: min-content;
}
</style>