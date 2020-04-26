<template>
  <div id="app">
    <header>
      <div>
        <h2 id="me">Mes Todos</h2>
      </div>
    </header>

    <Todo
      v-for="(todo, index) in todosAAfficher"
      :key="todo.id"
      :nom="todo.nom"
      :description="todo.description"
      :dateFin="todo.dateFin"
      :termine="todo.termine"
      :liste_id="todo.liste_id"
      @effacer-todo="effacerTodo(index, todo.id)"
      @modifier-etat-du-todo="payload => modifierEtat(index, payload)"
    >
    </Todo>

    <div>
      <AjoutUnTodo @ajouter-todo="ajouterTodo"></AjoutUnTodo>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Todo from "./components/Todo";
import AjoutUnTodo from "./components/AjoutUnTodo";
export default {
  name: "app",
  data() {
    return {
      modifierEtatDuTodo: false,
      todos: []
    };
  },
  components: {
    Todo,
    AjoutUnTodo
  },
  computed: {
    todosAAfficher() {
      if (!this.afficherUniquementLesTodosAjoute) {
        return this.todos;
      }
      return this.todos.filter(todo => !todo.termine);
    }
  },
  methods: {
    modifierEtat(indexDuTodo, nouvelEtat) {
      const copie = Object.assign({}, this.todos[indexDuTodo]);
      copie.termine = nouvelEtat.termine;
      axios
        .put(`http://localhost:3000/todos/${copie.id}`, copie)
        .then(reponse => {
          this.todos[indexDuTodo] = reponse.data;
        });
    },
  

    ajouterTodo(todoAAjouter) {
      const todoEnregistrer = Object.assign({}, todoAAjouter);
      todoEnregistrer.termine = false;
      axios
        .post(`http://localhost:3000/todos/`, todoEnregistrer)
        .then(reponse => {
          this.todos.push(reponse.data);
        });
    },
    effacerTodo(index, id) {
      axios.delete(`http://localhost:3000/todos/${id}`).then(() => {
        this.todos.splice(index, 1);
      });
    }
  },
  created() {
    axios.get(" http://localhost:3000/todos").then(reponse => {
      this.todos = reponse.data;
    });
  }
};
</script>

<style>
#me {
  color: rgb(255, 255, 255);
  padding-left: 60px;
  font-family: Arial, Helvetica, sans-serif;
}
header {
  display: flex;
  height: 30%;
  width: auto;
  background-color: rgb(0, 140, 255);
  top: 0%;
}

@media screen and (max-width: 700px) and (min-width: 200px) {
  header {
    width: 100%;
  }
  #app {

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    align-self: auto;
  }
}
</style>
