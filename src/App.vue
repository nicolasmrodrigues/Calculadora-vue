<script setup>
import { reactive } from 'vue';

const estado = reactive({
  numeroX: 0,
  numeroY: 0,
  resultado: 0,
  operacao: 'adição',
  simbolo: '+'
});

const atualizaNumeroX = (evento) => {
  estado.numeroX = Number(evento.target.value)
  atualizaResultado()
}

const atualizaNumeroY = (evento) => {
  estado.numeroY = Number(evento.target.value)
  atualizaResultado()
}

const atualizaResultado = () => {
  switch (estado.operacao) {
    case 'adição':
      estado.simbolo = '+'
      return estado.resultado = estado.numeroX + estado.numeroY;
    case 'subtração':
      estado.simbolo = '-'
      return estado.resultado = estado.numeroX - estado.numeroY;
    case 'multiplicação':
      estado.simbolo = 'x'
      return estado.resultado = estado.numeroX * estado.numeroY;
    case 'divisão':
      estado.simbolo = '÷'
      if (isNaN(estado.numeroX / estado.numeroY)) {
        return estado.resultado = 'Opercação inválida'
      }
      return estado.resultado = estado.numeroX / estado.numeroY;
  }
}

const atualizaOperacao = (evento) => {
  estado.operacao = evento.target.value;
  atualizaResultado();
}
</script>

<template>
  <div class="container mt-5">
    <h1 class="text-center">Calculadora Aritimética</h1>
    <form>
      <div class="row mt-5 justify-content-center">
        <div class="col-md-2">
          <input @keyup="atualizaNumeroX" @change="atualizaNumeroX" type="number" placeholder="Número 1"
            class="form-control">
        </div>
        <div class="col-md-1 text-center h4">{{ estado.simbolo }}</div>
        <div class="col-md-2">
          <input @keyup="atualizaNumeroY" @change="atualizaNumeroY" type="number" placeholder="Número 2"
            class="form-control">
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="atualizaOperacao">
            <option value="adição">adição</option>
            <option value="subtração">subtração</option>
            <option value="multiplicação">multiplicação</option>
            <option value="divisão">divisão</option>
          </select>
        </div>
        <div class="col-md-2 text-nowrap">
          <span class="align-middle lh-lg">Resultado: {{ estado.resultado }}</span>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped></style>
