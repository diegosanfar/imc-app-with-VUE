<template>
  <h1 class="label-title">Cálculo do IMC</h1>
  <h2 class="label-subtitle">Digite seu peso e altura para calcular o IMC</h2>

  <div class="div-imc">
    <span class="p-float-label">
      <InputText
        id="input-weight"
        type="number"
        v-model="weight"
        :disabled="imc"
      />
      <label for="input-weight">Peso (kg)</label>
    </span>
  </div>

  <div class="div-imc">
    <span class="p-float-label">
      <InputText
        id="input-height"
        type="number"
        v-model="height"
        :disabled="imc"
      />
      <label for="input-height">Altura (metros)</label>
    </span>
  </div>

  <div class="div-imc">
    <Button
      label="Calcular"
      @click="calculate"
      v-if="!imc"
      :disabled="!height || !weight || height <= 0 || weight <= 0"
    />
    <Button label="Calcular novamente" @click="clear" v-if="imc" />
  </div>

  <div v-if="imc" class="imc">
    <fieldset>
      <legend class="legend">IMC</legend>
      <p>{{ imc }}</p>
    </fieldset>
    <fieldset>
      <legend>Classificação</legend>
      <p>{{ classification }}</p>
    </fieldset>
  </div>
</template>

<script>
export default {
  data() {
    return {
      height: null,
      weight: null,
      imc: null,
      classification: "",
    };
  },
  methods: {
    calculate: function() {
      this.imc = (this.weight / Math.pow(this.height, 2)).toFixed(1);
      if (this.imc > 0 && this.imc < 18.5) {
        this.classification = "Magreza";
      } else if (this.imc >= 18.5 && this.imc < 25) {
        this.classification = "Normal";
      } else if (this.imc >= 25 && this.imc < 30) {
        this.classification = "Sobrepeso";
      } else if (this.imc >= 30 && this.imc < 40) {
        this.classification = "Obesidade";
      } else if (this.imc > 40) {
        this.classification = "Obesidade Grave";
      } else {
        this.classification = "Peso inválido.";
      }
    },
    clear() {
      this.height = null;
      this.weight = null;
      this.imc = null;
      this.classification = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
}
.div-imc {
  margin-top: 2em;
}
.label-title {
  font-size: 2rem;
}
.label-subtitle {
  font-size: 1.1rem;
}
span {
  position: relative;
  font-size: 1.2rem;
}
.imc {
  font-size: 22px;
}

p {
  font-size: 2rem;
}

fieldset {
  display: inline-block;
  text-align: center;
  box-sizing: border-box;
  width: 50%;
  height: 50%;
}

.p-float-label {
  display: inline-block !important;
  text-align: center;
}
</style>
