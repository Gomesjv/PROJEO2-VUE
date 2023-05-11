<script setup>
import { ref } from 'vue';


let valortotal = ref(0)
const produtos = ref([
  {
    id: 1,
    nome: 'Camiseta',
    preco: 49.90,
    quantidade: 0
  },
  {
    id: 2,
    nome: 'Calça',
    preco: 99.90,
    quantidade: 0
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.90,
    quantidade: 0
  },
  {
    id: 4,
    nome: 'Sapato',
    preco: 199.90,
    quantidade: 0
    },
  {
    id: 5,
    nome: 'Boné',
    preco: 29.90,
    quantidade: 0
  },
  {
    id: 6,
    nome: 'Óculos',
    preco: 99.90,
    quantidade: 0
  },
  {
    id: 7,
    nome: 'Relógio',
    preco: 299.90,
    quantidade: 0
  },
  {
    id: 8,
    nome: 'Bermuda',
    preco: 79.90,
    quantidade: 0
  },
  {
    id: 9,
    nome: 'Cueca',
    preco: 19.90,
    quantidade: 0
  },
  {
    id: 10,
    nome: 'Meia',
    preco: 9.90,
    quantidade: 0
  }
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
  item.quantidade = 0
}
function totalvalor(){
  for (let contador = 0; contador < carrinho.value.length; contador++) {
    valortotal.value = valortotal.value + carrinho.value[contador].totalitem  
  }
}
function limpacarrinho() {
  carrinho.value = []
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
      <li v-for="(item, index) in carrinho" :key="index">{{ item.nome }} {{avf(item.preco) }} {{
        item.quantidade
      }} valor total {{ avf(item.totalitem) }}
        <button @click="remover(index)">remover item</button>
      </li>
    </ul>
    <button @click="limpacarrinho()">limpar carrinho</button>
  </div>
  <ul>
    <li v-for="(item, index) in produtos" :key="index">Item: {{ item.nome }} Valor: {{ avf(item.preco) }}
      Quantidade: {{ item.quantidade }}
      <button @click="addcarrinho(item)">adicionar</button>
      <button @click="item.quantidade++">+</button>
      <button @click="item.quantidade--" v-if="item.quantidade > 0">-</button>
    </li>
  </ul>
</template>


<style scoped>

li{
 display: grid;
  align-items: center;
  margin-bottom: 10px;
  font-family: Arial, Helvetica, sans-serif;
  grid-template-columns: 1fr 2fr;
}
button{
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
  margin: 10px;
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
  letter-spacing: 1px;
  background: transparent;
  transition: ease-out 0.5s;
  border: 2px solid #725AC1;
  box-shadow: inset 0 0 0 0 #725AC1;
}
button:hover {
  color: white;
  box-shadow: inset 0 -100px 0 0 #725AC1;
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



