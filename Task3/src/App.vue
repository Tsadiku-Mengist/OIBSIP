<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-r from-teal-500 to-indigo-600 text-white">
    <div class="bg-white text-black rounded-lg shadow-lg p-8 max-w-md w-full">
      <h1 class="text-4xl font-bold mb-6 text-center">Temperature Converter</h1>

      
      <div class="mb-4">
        <input
          v-model.number="temperature"
          type="number"
          placeholder="Enter temperature"
          class="w-full px-4 py-3 rounded-lg shadow-sm border-gray-300 focus:ring-2 focus:ring-indigo-400 outline-none"
        />
        <p v-if="errorMessage" class="text-red-500 mt-2">{{ errorMessage }}</p>
      </div>

      
      <div class="mb-4">
        <label class="block mb-2">Select Input Unit</label>
        <select v-model="inputUnit" class="w-full px-4 py-3 rounded-lg shadow-sm border-gray-300 focus:ring-2 focus:ring-indigo-400 outline-none">
          <option value="Celsius">Celsius</option>
          <option value="Fahrenheit">Fahrenheit</option>
          <option value="Kelvin">Kelvin</option>
        </select>
      </div>

    
      <div class="mb-6">
        <label class="block mb-2">Select Output Unit</label>
        <select v-model="outputUnit" class="w-full px-4 py-3 rounded-lg shadow-sm border-gray-300 focus:ring-2 focus:ring-indigo-400 outline-none">
          <option value="Celsius">Celsius</option>
          <option value="Fahrenheit">Fahrenheit</option>
          <option value="Kelvin">Kelvin</option>
        </select>
      </div>

    
      <button
        @click="convertTemperature"
        class="w-full py-3 bg-gradient-to-r from-teal-400 to-indigo-500 text-white font-semibold rounded-lg shadow-md hover:from-indigo-500 hover:to-teal-400 focus:ring-2 focus:ring-indigo-500 outline-none"
      >
        Convert
      </button>

      
      <div v-if="result !== null" class="mt-6 text-xl text-center font-semibold">
        <p>Converted Temperature: {{ result }}° {{ outputUnit }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      temperature: null, 
      inputUnit: 'Celsius', 
      outputUnit: 'Fahrenheit', 
      result: null, 
      errorMessage: '', 
    };
  },
  methods: {
    
    convertTemperature() {
      
      if (this.temperature === null || isNaN(this.temperature)) {
        this.errorMessage = 'Please enter a valid temperature.';
        this.result = null;
        return;
      }

      this.errorMessage = ''; 
      const temp = parseFloat(this.temperature);

      
      if (this.inputUnit === this.outputUnit) {
        this.result = temp;
      } else if (this.inputUnit === 'Celsius') {
        if (this.outputUnit === 'Fahrenheit') {
          this.result = (temp * 9) / 5 + 32;
        } else if (this.outputUnit === 'Kelvin') {
          this.result = temp + 273.15;
        }
      } else if (this.inputUnit === 'Fahrenheit') {
        if (this.outputUnit === 'Celsius') {
          this.result = ((temp - 32) * 5) / 9;
        } else if (this.outputUnit === 'Kelvin') {
          this.result = ((temp - 32) * 5) / 9 + 273.15;
        }
      } else if (this.inputUnit === 'Kelvin') {
        if (this.outputUnit === 'Celsius') {
          this.result = temp - 273.15;
        } else if (this.outputUnit === 'Fahrenheit') {
          this.result = (temp - 273.15) * 9 / 5 + 32;
        }
      }
    },
  },
};
</script>
