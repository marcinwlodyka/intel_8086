<template>
  <div class="md:h-screen w-full flex flex-col-reverse md:flex-row bg-black p-2">
    <div class="auto md:w-1/2 lg:w-2/3 h-full flex flex-col">
      <div class="flex flex-col justify-center items-center h-auto md:h-1/2 panel-border">
        <ul class="flex flex-row flex-wrap flex-grow">
          <li 
            v-for="(input, i) in inputs"
            :key="i"
            class="w-full lg:w-1/2 my-2 flex flex-row justify-center"
          >
            <HexInput
              :name="input.name"
              @send="(n) => input.value = n"
              class="uppercase"
            />
          </li>
        </ul>

        <div class="flex flex-row">
          <button class="mx-1" @click="saveRegisters()">Save</button>
          <button class="mx-1" @click="resetRegisters()">Reset</button>
          <button class="mx-1" @click="randomRegisters()">Random</button>
        </div>
      </div>

      <div class="h-auto md:h-1/2 panel-border flex flex-col justify-evenly items-center">
        <div class="flex flex-row justify-evenly w-full">
          <Select 
            name="From" 
            :options="inputs" 
            @input="indexFrom = $event" 
            class="m-1"
          />
          <Select 
            name="To" 
            :options="inputs" 
            @input="indexTo = $event" 
            class="m-1"
          />
        </div>
        
        <Select
          name="Instruction"
          :options="instructionList"
          @input="selectedInstruction = $event"
          class="m-1"
        />

        <button @click="instructionList[selectedInstruction].instruction(indexFrom, indexTo)" class="m-1">Simulate</button>
      </div>
    </div>
    <div class="h-screen md:h-auto md:w-1/2 lg:w-1/3 flex justify-center items-center panel-border">
      <div class="w-full h-full flex flex-col bg-black p-8 rounded-xl">
        <ul class="text-white flex flex-row text-2xl text-center">
          <li class="text-black">A</li>
          <li class="flex-grow">H</li>
          <li class="flex-grow">L</li>
        </ul>
        <div class="flex flex-grow">
          <ul class="h-full flex-shrink temp flex flex-row flex-wrap justify-center items-center text-white mr-2">
            <li 
              v-for="(item, i) in [ 'A', 'B', 'C', 'D' ]" 
              :key="i"
              class="text-2xl text-right w-full"
            >
              {{ item }}
            </li>
          </ul>
          <ul class="h-full flex flex-row flex-wrap justify-center items-center flex-grow">
            <li
              v-for="(register, i) in registers"
              :key="i"
              class="w-1/2 text-center text-2xl bg-white rounded-full border-4 border-black"
            >
              {{ register }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Select from '@/components/Select.vue';
import HexInput from '@/components/HexInput.vue';

export default {
  components: { Select, HexInput },
  data() {
    return {
      inputs: [
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
      ],
      registers: Array(8).fill('00000000'),

      genRanHex: size => [...Array(size)].map(() => Math.floor(Math.random() * 16).toString(16)).join(''),

      indexFrom: '0',
      indexTo: '0',
      selectedInstruction: '0',
      temp: '0',

      instructionList: [
        {
          name: 'mov',
          instruction: (from, to) => {
            Vue.set(this.registers, to, this.registers[from]);
          } 
        },
        {
          name: 'exch',
          instruction: (from, to) => {
            const temp = this.registers[from];

            Vue.set(this.registers, from, this.registers[to]);
            Vue.set(this.registers, to, temp);
          }
        }
      ]
    }
  },
  methods: {
    saveRegisters() {
      this.registers = [];

      this.inputs.forEach(input => {
        if(input.value == '')
          this.registers.push('00000000');
        else
          this.registers.push(input.value);
      });

      console.log(this.registers);
      console.log(this.inputs.value);
    },
    resetRegisters() {
      this.registers = Array(8).fill('00000000')
    },
    randomRegisters() {
      this.registers = []
      
      this.inputs.forEach(() => {
        this.registers.push(this.genRanHex(8));
      });
      
      console.log(this.registers);
    },

    test() {
      console.log('test');
    }
  }
}
</script>

<style scoped>
input,
button {
  background-color: white;
  border: black solid 2px;
  border-radius: 10rem;
  padding: 0.25rem 1rem;
  width: min-content;
  height: min-content;
}
button:hover {
  background-color: black;
  color: white;
}
.panel-border {
  background-color: white;
  border-radius: 0.75rem;
  margin: 0.5rem;
  padding: 2rem;
}
.temp {
  width: min-content;
}
</style>