<template>
  <div class="container">
    <section class="todo">
      <input
        type="checkbox"
        v-model="isTermine"
        :checked="termine"
        @change="modifierEtatDuTodo"
      />
      {{ nom }}<br />
      {{ description }}<br />
      {{ dateFin }}<br />
    </section>

    <div id="effacer">
      <button @click="effacer">Effacer</button>
    </div>
  </div>
</template>

<script>
import AjoutUnTodoVue from "./AjoutUnTodo.vue";
export default {
  name: "Todo",
  data() {
    return {
      nouveauTodo: {
        nom: "",
        description: "",
        dateFin: ""
      }
    };
  },
  props: {
    nom: {
      type: String
    },
    description: {
      type: String
    },
    dateFin: {
      type: String
    },
    termine: {
      type: Boolean
    },
    liste_id: {
      type: Number
    }
  },
  data() {
    return {
      isTermine: this.termine
    };
  },
  methods: {
    modifierEtatDuTodo() {
      this.$emit("modifier-etat-du-todo", {
        termine: !this.termine
      });
    },
    effacer() {
      this.$emit("effacer-todo", {});
    }
  },
  computed: {
    affichageDispo() {
      if (this.isTermine === false) {
        return "disponible";
      } else {
        return "termine";
      }
    }
  }
};
</script>

<style>
@media screen and (max-width: 700px) and (min-width: 200px) {

    .todo{
        width: 100%;
         border-bottom:1px solid;
         margin: 0;
    }
  .container {

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    align-self: auto;
    width: 100%;
  }
}
.container {
  padding: 10px;
}
.todo {
  margin: 50px;
  display: flex;
  justify-items: flex-start;
  align-self: flex-start;
  justify-items: flex-start;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  border-bottom: black solid 0.5px;
}
#effacer {
  display: flex;
  justify-content: flex-end;
  align-self: flex-end;
  justify-items: flex-end;
  text-justify: auto;
  text-align: center;
  font-size: 10pt;
  margin-right: 40px;
  margin-bottom: 10px;
  border-radius: 5%;
  width: 60pxs;
  height: 20px;
  bottom: 0%;
}
</style>
