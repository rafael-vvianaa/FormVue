<template>
  <div id="app">
    <!-- <Cadastro /> -->
    <form @submit="postData" method="post">
      <fieldset>
        <fieldset class="grupo">
          <div class="campo">
            <label for="matriculaEstudante">Matricula estudante: </label>
            <input
              type="text"
              id="matriculaEstudante"
              name="matriculaEstudante"
              style="width: 10em"
              v-model="posts.matriculaEstudante"
            />
          </div>
          <div class="campo">
            <label for="nomeEstudante">Nome Estudante: </label>
            <input
              type="text"
              id="nomeEstudante"
              name="nomeEstudante"
              style="width: 10em"
              v-model="posts.nomeEstudante"
            />
          </div>
        </fieldset>
        <div class="campo">
          <label for="nomeCliente">Nome Cliente</label>
          <input
            type="text"
            id="nomeCliente"
            name="nomeCliente"
            style="width: 20em"
            v-model="posts.nomeCliente"
          />
        </div>
        <div class="campo">
          <label for="enderecoCliente">Endereço cliente</label>
          <input
            type="text"
            id="enderecoCliente"
            name="enderecoCliente"
            style="width: 10em"
            v-model="posts.enderecoCliente"
          />
        </div>

        <fieldset>
          <div>
            <label for="Estado">Estado: </label>
            <div>
              <select>
                <option v-for="(estado, index) in estados" :key="index.id">{{
                  estado.nome
                }}</option>
              </select>
            </div>
          </div>
          <!-- <div class="campo">
            <label for="Cidade">Cidade</label>
            <select name="Cidade" id="Cidade">
              <option value="">-{{}}</option>
              <option value="PR">P</option>
            </select>
          </div> -->
        </fieldset>
        <button type="submit" name="submit">Cadastrar</button>
      </fieldset>
    </form>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);
export default {
  name: "App",
  data() {
    return {
      estados: [],
      posts: {
        matriculaEstudante: null,
        nomeEstudante: null,
        nomeCliente: null,
        enderecoCliente: null,
      },
    };
  },
  created: function() {
    axios
      .get("https://servicodados.ibge.gov.br/api/v1/localidades/estados")
      .then((res) => {
        this.estados = res.data;
        console.log(this.estados);
      });
  },
  methods: {
    postData(e) {
      this.axios
        .post("https://web-unit.herokuapp.com/cliente", this.posts)
        .then((result) => {
          console.warn(result);
        });
      e.preventDefault();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

