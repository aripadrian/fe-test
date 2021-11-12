<template>
  <div id="app" class="bg-pink-600 min-h-screen min-w-screen">
    <div class="container p-4">
      <div class="bg-white rounded-xl p-4">
        <h1 class="font-bold text-3xl w-full text-center ">Kalkulet</h1>
        <h3 class="text-center text-pink-500">Result</h3>
        <p class="text-2xl font-bold text-purple-600 text-center">{{result}}</p>
        <div class="mt-12 flex flex-col gap-4">
        <div class="flex gap-2 items-center">
          <input type="number" class="p-3 border-2 rounded-md w-10/12 focus:outline-none focus:border-pink-400" v-model="input[0].value">
          <input type="checkbox" class="mx-auto"  v-model="input[0].checklist">
        </div>
         <div class="flex gap-2 items-center">
          <input type="number" class="p-3 border-2 rounded-md w-10/12 focus:outline-none focus:border-pink-400" v-model="input[1].value">
          <input type="checkbox" class="mx-auto"  v-model="input[1].checklist">
        </div>
         <div class="flex gap-2 items-center">
          <input type="number" class="p-3 border-2 rounded-md w-10/12 focus:outline-none focus:border-pink-400" v-model="input[2].value">
          <input type="checkbox" class="mx-auto" v-model="input[2].checklist">
        </div>
        </div>

        <!-- operator begin -->
        <div class="grid grid-cols-4 gap-2 mt-4">
         <button :class="{'bg-blue-600':operator==='+'}" class="py-6 font-bold text-2xl border-2 border-blue-600 rounded-lg focus:outline-none" @click.prevent="setOperator('+')">+</button>
         <button :class="{'bg-red-600':operator==='-'}" class="py-6 font-bold text-2xl border-2 border-red-600 rounded-lg focus:outline-none" @click.prevent="setOperator('-')">-</button>
         <button :class="{'bg-yellow-600':operator==='x'}" class="py-6 font-bold text-2xl border-2 border-yellow-600   rounded-lg focus:outline-none" @click.prevent="setOperator('x')">x</button>
         <button :class="{'text-white bg-green-600':operator==='/'}" class="py-6 font-bold text-2xl border-2 border-green-600 rounded-lg focus:outline-none" @click.prevent="setOperator('/')">/</button>
        </div>
        <!-- end operator -->

        <div>
       
        </div>
        <!-- button result -->
        <div class="flex gap-2 mt-4">
          <button class="w-4/12 py-6 border-2 text-purple-600 border-purple-600 text-white text-xl rounded-lg focus:outline-none" @click.prevent="reset">
          reset</button>
          <button @click.prevent="calculate" class="w-8/12 py-6 bg-purple-700 text-white text-xl rounded-lg focus:outline-none">
            result
          </button>
        </div>
        <!-- end button -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {},
  data() {
    return {
      input: [
        {
          value: '',
          checklist: false
        },
        {
          value: '',
          checklist: false
        },
       {
          value: '',
          checklist: false
        },
      ],
      operator: null,
      result: 0,
      error: []
    }
  },
  methods: {
    setOperator(value) {
      this.operator = value
    },
  calculate() {
    this.result = 0
    let number = []
    let result = 0
    this.input.forEach(e => {
      if(e.checklist) {
        number.push(e.value)
      }
    });

  //  when input only 1
   if(number.length<2) {
     alert('Minimal 2 inputan yang checklist !')
   }

  //  when operator null
    if(this.operator===null) { 
     alert('Operator belum dipilih !')
    }

    switch (this.operator) {
      case '+':
        result = parseInt(number[0])
        for (let i = 0; i < number.length-1; i++) {
          result = result + parseInt(number[i+1])
        }
        break;

      case '-':
        result = parseInt(number[0])
        for (let i = 0; i < number.length-1; i++) {
          result = result - parseInt(number[i+1])
        }
        break;

      case 'x':
       result = parseInt(number[0])
        for (let i = 0; i < number.length-1; i++) {
          result = result * parseInt(number[i+1])
        }
        break;

      case '/':
        result = parseInt(number[0])
        for (let i = 0; i < number.length-1; i++) {
          result = result / parseInt(number[i+1])
        }
        break;
    
      default:
        break;
    }

    // set result value
    if(result) {
      this.result = result
    }
  },
    reset() {
      Object.assign(this.$data, this.$options.data());
    }
  }
}
</script>

<style src="./assets/css/style.css"></style>

