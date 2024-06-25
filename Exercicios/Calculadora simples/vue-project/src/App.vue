<script setup>
import { ref, reactive, computed } from 'vue';

const primeiroNumero = ref(0);
const segundoNumero = ref(0);
const operacao = ref('adicao');

const estado = reactive({
  adicao: '+',
  subtracao: '-',
  divisao: '/',
  multiplicacao: '*'
})

const resultado = computed(() => {
  const num1 = parseFloat(primeiroNumero.value);
  const num2 = parseFloat(segundoNumero.value);
  switch (operacao.value) {
    case 'adicao':
      return num1 + num2; 
    case 'subtracao':
      return num1 - num2; 
    case 'divisao':
      return num2 !== 0 ? num1 / num2 : 'Erro: Divisão por zero'; 
    case 'multiplicacao':
      return num1 * num2; 
    default:
      return 0; 
  }
});

</script>

<template>
    <div class="container">
    <h1>Calculadora</h1>
    <div>
      <p>Escolha a operação desejada</p>
      <select v-model="operacao">
        <option value="adicao">{{ estado.adicao }}</option>
        <option value="subtracao">{{ estado.subtracao }}</option>
        <option value="divisao">{{ estado.divisao }}</option>
        <option value="multiplicacao">{{ estado.multiplicacao }}</option>
      </select>
    </div>
    <div id="calc">
      <input v-model.number="primeiroNumero" type="number" min="0" placeholder="Digite o primeiro número">
      <span>{{ estado[operacao] }}</span>
      <input v-model.number="segundoNumero" type="number" min="0" placeholder="Digite o segundo número">
    </div>
    <div>
      <h2>Resultado: {{ resultado }}</h2>
    </div>
  </div>

</template>

<style scoped>
.container {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  text-align: center;
  background-color: rgba(192, 192, 192, 0.233);
}

input {
  width: 80px;
  margin: 0 10px;
  padding: 5px;
  border-radius: 4px;
}

select {
  margin-bottom: 20px;
}

h2 {
  margin-top: 20px;
}
</style>
