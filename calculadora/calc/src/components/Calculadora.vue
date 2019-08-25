<template>
  <div class="calculadora">
    <div @click="simbolo" class="display">{{ current || '0' }}</div>
    <div @click="limpa" class="btn">C</div>
    <div @click="sinal" class="btn">+/-</div>
    <div @click="porcent" class="btn">%</div>

    <div @click="dividir" class="btn operator">&divide;</div>

    <div @click="numeros(7)" class="btn">7</div>
    <div @click="numeros(8)" class="btn">8</div>
    <div @click="numeros(9)" class="btn">9</div>

    <div @click="multi" class="btn operator">x</div>

    <div @click="numeros(4)" class="btn">4</div>
    <div @click="numeros(5)" class="btn">5</div>
    <div @click="numeros(6)" class="btn">6</div>

    <div @click="menos" class="btn operator">-</div>

    <div @click="numeros(1)" class="btn">1</div>
    <div @click="numeros(2)" class="btn">2</div>
    <div @click="numeros(3)" class="btn">3</div>

    <div @click="soma" class="btn operator">+</div>

    <div @click="numeros(0)" class="btn zero">0</div>
    <div @click="ponto" class="btn">.</div>

    <div @click="igual" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculadora',
  data(){
    return {
      primeiroNum: null,
      current: '',
      operador: null,
      operadorClicado: false
    }
  },
  methods: {
    limpa(){
      this.current = '';
    },
    sinal(){
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    porcent(){
      this.current = `${parseFloat(this.current) / 100}`
    },
    numeros(num){
      if (this.operadorClicado) {
        this.current = '';
        this.operadorClicado = false;
      }
      this.current = `${this.current}${num}`;
    },
    ponto(){
      if (this.current.indexOf('.') === -1) {
        this.numeros('.');
      }
    },
    setPrimeroNum(){
      this.primeiroNum = this.current;
      this.operadorClicado = true;
    },
    dividir(){
      this.operador = (a,b) => a / b;
      this.setPrimeroNum();      
    },
    multi(){
      this.operador = (a,b) => a * b;
      this.setPrimeroNum();
    },
    menos(){
      this.operador = (a,b) => a - b;
      this.setPrimeroNum();
    },
    soma(){
      this.operador = (a,b) => a + b;
      this.setPrimeroNum();
    },
    igual(){
      this.current = `${this.operador(
        parseFloat(this.current), 
        parseFloat(this.primeiroNum)
        )}`;
      this.primeiroNum = null;
      
    }
 }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculadora{
    max-width: 400px;
    margin: 0 auto;
    font-size: 40px;
    display: grid;
    grid-template-columns:  repeat(4, 1rf);
    grid-auto-rows: minmax(50px, auto);
  }

  .display{
    grid-column: 1 / 5;
    background: #333;
    color: #fff;
  }

  .zero{
    grid-column: 1 / 3;
  }

  .btn{
    background-color: #f2f2f2;
    border: 1px solid #999;
    cursor: pointer;
  }

  .btn:hover{
    background: #ccc;
  }

  .operator{
    background: orange;
    color: #fff;
  }

  .operator:hover{
    background: darkorange;
  }
</style>