<script>
export default {
  data() {
    return {
      porcentagens: ['0', '5', '10', '15', '20', '25', '30'],
      porcentagemAtiva: '0',
      quantidadePessoas: 0,
      valorConta: 0,
      valorGorjeta: 0,
      total: 0,
    };
  },
  computed: {
    formValid() {
      const { valorConta, porcentagemAtiva } = this;
      return +this.valorConta > 0 && +this.porcentagemAtiva > 0;
    },
  },
  methods: {
    calculate() {
      const { quantidadePessoas, valorConta, porcentagemAtiva } = this;
      this.valorGorjeta = this.valorGorjeta * (porcentagemAtiva / 100);
      this.total = (valorConta * (1 + porcentagemAtiva /100) / quantidadePessoas)
    },
  },
};
</script>

<template>
<div class="container">
  <form @submit.prevent="calculate">
    <div class="divisor">
      <label>Valor da conta:</label>
      R$<input type="number" v-model.number="valorConta">
    </div>
    <div class="divisor">
      <label>Quantidade de pessoas:</label>
      <input type="number" v-model.number="quantidadePessoas">
    </div>
    <div class="divisor">
      <label>Gorjeta:</label>
      <select v-model="porcentagemAtiva" @change="onChange">
        <option :value="porcentagem" v-for="porcentagem in porcentagens">{{ porcentagem }}%</option>
      </select>
    </div>
    <div class="divisor">
      <button type="submit">Calcular</button>
    </div>
    <div>
      <p>Total por pessoa: R${{ total.toFixed(2) }}</p>
    </div>
  </form>
</div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap");

.container {
  font-family: "Poppins", sans-serif;
  font-size: 0.938rem;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  background-color: hsl(var(207), 8%, 13%);
  
}

.divisor {
  padding: .5rem;
}

button,
input,
textarea,
select {
  font-family: "Poppins", sans-serif;
  font-size: 0.938rem;
}

button {
  cursor: pointer;
  border: none;
  outline: none;
  display: inline-block;
  background-color: hsl(207, 90%, 72%);
  color: hsl(207, 8%, 13%);
  padding: 0.75rem 1rem;
  border-radius: 0.5rem;
  font-weight: var(--font-medium);
}

button:hover {
  background-color: hsl(207, 90%, 55%);
  color: hsl(207, 8%, 13%);
  transition: .35s;
}

form {
  background-color: hsl(var(207), 8%, 13%);
  border-radius: 1rem;
  padding: 3em;
  height: 22rem;
  backdrop-filter: blur(10px);
  box-shadow: 20px 20px 40px -6px rgba(0,0,0,0.2);
  text-align: left;
  position: relative;
  transition: all 0.2s ease-in-out;
}

input, select {
  top: 0;
  left: 0;
  border: 2px solid var(--text-color-light);
  background: none;
  color: var(--text-color);
  outline: none;
  padding: .3rem;
  border-radius: 0.75rem;
  z-index: 1;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type=number] {
  -moz-appearance: textfield;
}

select option {
    margin: 40px;
    background: hsl(207, 90%, 72%);
    color: #fff;
    text-shadow: 0 1px 0 rgba(0, 0, 0, 0.4);
}

label {
  position: relative;
  padding: 0;
  margin: 0;
  color: #fff;
  opacity: 0.7;
  font-size: 1.4rem;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
  text-align: justify
}


p{
  text-decoration: none;
  color: #ddd;
  font-size: 12px;
  padding-top: 1.6rem;
}
</style>