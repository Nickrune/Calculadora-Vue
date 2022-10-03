<script>
export default {   
  data() {
    return {
      anterior: null,
      atual: '',
      operador: null,
      operadorClicado: false,
    }
  },
   methods: {
    clear() {
      this.atual = '';
    },
    sinal() {
      this.atual = this.atual.charAt(0) === '-'?
      this.atual.slice(1) : `-${this.atual}`;
    },
    porcentagem() {
      this.atual = `${parseFloat(this.atual) / 100}`;
    },
    adicionarNumero(number){
      if (this.operadorClicado) {
        this.atual = '';
        this.operadorClicado = false;
      }
      this.atual = `${this.atual}${number}`;
    },
    ponto() {
      if (this.atual.indexOf('.') === -1) {
        this.adicionarNumero('.')
      }
    },
    defineAnterior() {
      this.anterior = this.atual;
      this.operadorClicado = true;
    },
    divide() {
      this.operador = (a, b) => b / a;
      this.defineAnterior();
    },
    multiplica(){
      this.operador = (a, b) => a * b;
      this.defineAnterior();
    },
    subtrai(){
      this.operador = (a, b) => b - a;
      this.defineAnterior();
    },
    soma(){
      this.operador = (a, b) => a + b;
      this.defineAnterior();
    },
    igual() {
      this.atual = `${this.operador(parseFloat(this.atual),parseFloat(this.anterior))}`;
      this.anterior = null;
    }
   }
}
  

</script>

<template>
  <h1 class="titulo"> Calculadora Em vue</h1>
  
  <div class="calculadora">
    
    <div class="display">{{atual || 0}}</div>
    <div @click= "clear" class="button">C</div>
    <div @click= "sinal" class="button">+/-</div>
    <div @click= "porcentagem" class="button ">%</div>
    <div @click= "divide" class="button operador">/</div>  
    <div @click="adicionarNumero('7')" class="button">7</div>
    <div @click="adicionarNumero('8')" class="button">8</div>
    <div @click="adicionarNumero('9')" class="button">9</div>
    <div @click= "multiplica" class="button operador">X</div>
    <div @click="adicionarNumero('4')" class="button">4</div>
    <div @click="adicionarNumero('5')" class="button">5</div>
    <div @click="adicionarNumero('6')" class="button">6</div>
    <div @click= "subtrai" class="button operador">-</div>
    <div @click="adicionarNumero('1')" class="button">1</div>
    <div @click="adicionarNumero('2')" class="button">2</div>
    <div @click="adicionarNumero('3')" class="button">3</div>
    <div @click= "soma" class="button operador">+</div>
    <div @click="adicionarNumero('0')" class="buttonzero">0</div>
    <div @click="ponto" class="button">.</div>
    <div @click="igual" class="button operador">=</div>
  </div>
</template>

<style scoped>
.calculadora {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display:grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color:tomato;
  
}

.buttonzero {
  grid-column: 1 / 3;
  background-color: gray;
}
.button {
  background-color: gray;
  border: 1px solid #333 ;
  cursor: pointer;
}

.operador {
  background-color: orange;
  color: aliceblue;
}

.titulo{
  margin: 0 auto;
  display:flex;
  padding:0.4cm
  
}
</style>
