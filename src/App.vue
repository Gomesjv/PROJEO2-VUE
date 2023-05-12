<script setup>
import { ref } from 'vue';


let valortotal = ref(0)
const produtos = ref([
  {
    id: 1,
    nome: 'Camiseta',
    preco: 49.90,
    quantidade: 1
  },
  {
    id: 2,
    nome: 'Calça',
    preco: 99.90,
    quantidade: 1
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.90,
    quantidade: 1
  },
  {
    id: 4,
    nome: 'Sapato',
    preco: 199.90,
    quantidade: 1
  },
  {
    id: 5,
    nome: 'Boné',
    preco: 29.90,
    quantidade: 1
  },
  {
    id: 6,
    nome: 'Óculos',
    preco: 99.90,
    quantidade: 1
  },

])
let carrinho = ref([])
function addcarrinho(item) {
  carrinho.value.push({
    codigo: item.id,
    nome: item.nome,
    preco: item.preco,
    quantidade: item.quantidade,
    totalitem: item.preco * item.quantidade
  })
  totalvalor()
  item.quantidade = 1
}

function totalvalor() {
  valortotal.value = 0
  for (let contador = 0; contador < carrinho.value.length; contador++) {
    valortotal.value = valortotal.value + carrinho.value[contador].totalitem
  }
}
function limpacarrinho() {
  carrinho.value = []
  valortotal.value = 0
}
function remover(index) {
  carrinho.value.splice(index, 1)
}
const avf = (value) => "R$ " + value.toFixed(2).replace('.', ',')
</script>

<template>
  <div class="carrinho">
    <h1>CARRINHO {{ avf(valortotal) }}</h1>
    <ul>
      <li v-for="(item, index) in carrinho" :key="index">
        <p> Item : {{ item.nome }}</p>
        <p> Preço : {{ avf(item.preco) }}</p>
        <p> Quantidade : {{ item.quantidade }}</p>
        valor total {{ avf(item.totalitem) }}
        <button @click="remover(index)">remover item</button>
      </li>
    </ul>
    <button @click="limpacarrinho()">limpar carrinho</button>
  </div>
  <ul>

    <li v-for="(item, index) in produtos" :key="index" class="a">
      <p>Item : {{ item.nome }}</p>
      <p>Valor : {{ avf(item.preco) }}</p>
      <p> Quantidade : {{ item.quantidade }}</p>

      <button @click="addcarrinho(item)">adicionar</button>
      <p><button @click="item.quantidade++">+</button></p>


    </li>
  </ul>
</template>


<style scoped>
ul {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;

}

li {
  display: grid;
  border: 4px solid black;
  height: 230px;
  width: 150px;
  padding: 20px;
  border-radius: 20px;
  list-style: none;
  margin: 40px;
}

p {
  margin-bottom: 10px;
  font-family: Arial, Helvetica, sans-serif;
}


button {
  height: 30px;
  width: 140px;
  border-radius: 10px;
  border: none;
  background-color: #ccc;
  cursor: pointer;
  border: none;
  color: black;
  padding: 5px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: -5px;
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
  letter-spacing: 1px;
  background: transparent;
  transition: ease-out 1.5s;
  border: 2px solid #000000;
  box-shadow: inset 0 0 0 0 #000000;
}

button:hover {
  color: white;
  box-shadow: inset 0 -100px 0 0 #000000;
}

button:active {
  transform: scale(0.9);
}

h1 {
  font-size: 32px;
  font-weight: bold;
  font-style: italic;
  color: #333;
  font-family: Arial, Helvetica, sans-serif;

}
</style>



