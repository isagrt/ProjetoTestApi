<script>
import axios from "axios";
export default {
  data() {
    return {
      cep: "",
      endereco: {},
    };
  },
  methods: {
    async search() {
      const url = `https://viacep.com.br/ws/${this.cep}/json/`;
      const { data } = await axios.get(url);
      this.endereco = data;
    },
  },
};
</script>

<template>
  <main>
    <forms class="form" @submit.prevent="search">
      <h1>Buscar CEP</h1>
      <div class="cepinfo">
        <label for="cep">CEP</label>
        <input type="text" id="cep" v-model="cep" />
      </div>
      <button @click="search()" type="submit">buscar</button>
    </forms>
    <form class="infofinal">
      <label for="rua">Rua</label>
      <input type="text" v-model="endereco.logradouro" />
      <label for="numero">Número</label>
      <input type="text" v-model="endereco.numero" />
      <label for="bairro">Bairro</label>
      <input type="text" v-model="endereco.bairro" />
    </form>

    {{ endereco }}
  </main>
</template>

<style>
.infofinal {
  display: flex;
  flex-direction: column;
}
.form {
  display: flex;
  flex-direction: column;

  flex-wrap: wrap;
  align-content: center;
}
</style>
