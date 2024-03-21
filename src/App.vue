<script setup>
import { reactive } from 'vue';

const estado = reactive({
    primeiroNumero: '',
    segundoNumero: '',
    operacoes: {
        soma: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a , b) => a * b,
        divisao: (a ,b) => (b !== 0 ? a / b: 'Divisão por zero'),
    },
    resultado: 0,
});

const calcularResultado = () => {
    const { primeiroNumero, segundoNumero, operacaoMatematica} = estado;
    estado.resultado = estado.operacoes[operacaoMatematica](parseFloat(primeiroNumero), parseFloat(segundoNumero));
};
</script>


<template>
  <div class="container p-5 bg-light rounded-3">
  <header>
  <div class="row">
          <h1 class="mb-4">Calculadora Aritimética</h1>
          <div class="col-md-2">
          <input type="text" v-model="estado.primeiroNumero" placeholder="Digite o primeiro valor" @input="calcularResultado" required>
          </div>
          <div class="col-md-2">
          <input type="text" v-model="estado.segundoNumero" placeholder="Digite o segundo valor" @input="calcularResultado" required>
          </div>
          <div class="col-md-2">
          <select v-model="estado.operacaoMatematica" @change="calcularResultado">
          <option value="soma">+</option>
          <option value="subtracao">-</option>
          <option value="divisao">/</option>
          <option value="multiplicacao">X</option>
          </select>
      </div>
  </div>
  </header>
  </div><!--container-->
  <div class="container mt-5">
  <main>
      <span v-if="!estado.operacaoMatematica">Para começar digite 2 números e selecione a operação na caixa ao lado [ v]</span>
      <span v-else-if="(estado.resultado >= 0 || estado.resultado < 0)" class="sucess wd-p">Resultado : {{ estado.resultado }}</span>
      <span v-else="estado.resultado = 'string'" class="error wd-p">Favor digitar um número nos campos e selecione uma operação na caixa ao lado [ ]!</span>
  </main>
  </div>
</template>
<style scoped>
  .wd-p {
      max-width: 300px;
      font-weight: bold;
  }

  .sucess {
      color: green;
  }

  .error {
      color: red;
  }
</style>

