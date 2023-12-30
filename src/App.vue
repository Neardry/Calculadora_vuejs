<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'soma',
  valor1: 0,
  valor2: 0,
  resposta: 0
});



const getFiltro = () => {
  const { filtro, valor1, valor2 } = estado;

  switch(filtro) {
    case 'soma': 
    estado.resposta = valor1 + valor2;
        break;
    case 'subtracao':
    estado.resposta = valor1 - valor2;
        break
      case 'divisao':
        if(valor2 == 0) {
          estado.resposta = "Impossível dividir por zero"
        } else {
          estado.resposta = valor1 / valor2;          
      }
        break
        case 'multiplicacao':
        estado.resposta = valor1 * valor2;
        break
  }
}

const qualFiltro = evento => { estado.filtro = evento.target.value;
getFiltro();
};




</script>

<template>
  <div class="container">
    <header class="pt-5">
      <h1 class="text-center">Calculadora aritmética</h1>
    </header>
    <div class="form-control bg-light d-flex justify-content-center align-items-center">
      <input @keyup="getFiltro"  v-model="estado.valor1" type="number">
      <select @change="qualFiltro" class="m-5">
        <option value="soma">+</option>
        <option value="subtracao">-</option>
        <option value="divisao">/</option>
        <option value="multiplicacao">*</option>
      </select>
      <input @keyup="getFiltro"  v-model="estado.valor2" type="number">
      <span class="ms-3 me-3">=</span>
      <span>{{ estado.resposta }}</span>
    </div>
  </div>
</template>

<style scoped>

</style>
