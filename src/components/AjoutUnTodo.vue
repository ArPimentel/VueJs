<template>
  <div id="bloque">
    <form @submit.prevent>
      <h4>Ajouter un todo</h4>
      <div id="label">
        <div>
          <label>
            <input type="text" v-model="nouveauTodo.nom" placeholder="Nom" />
          </label>
          <label>
            <input
              type="text"
              v-model="nouveauTodo.description"
              placeholder="Description"
            />
          </label>
          <label>
            <input
              type="text"
              v-model="nouveauTodo.dateFin"
              placeholder="Date"
            />
          </label>
        </div>
        <div class="button">
          <button :disabled="!todoValide" @click="ajouter">Ajouter</button>
          <button :disabled="!todoValide" @click="annuler">Annuler</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AjoutUnTodo",
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
  computed: {
    todoValide() {
      return (
        this.nouveauTodo.nom &&
        this.nouveauTodo.description &&
        this.nouveauTodo.dateFin
      );
    }
  },
  methods: {
    ajouter() {
      this.$emit("ajouter-todo", {
        ...this.nouveauTodo
      });
    },
    annuler() {
      this.nouveauTodo.nom = "";
      this.nouveauTodo.description = "";
      this.nouveauTodo.dateFin = "";
    }
  }
};
</script>

<style>
@media screen and (max-width: 700px) and (min-width: 200px) {
  #label {
    display: flex;
    flex-direction: column;
  }
  form {
    width: 100%;
  }
  #bloque {
    border: 0.5px solid black;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    align-self: auto;
    width: 100%;
    margin: auto;
  }
}
#bloque {
  display: flex;
  justify-items: center;
  align-self: center;
  justify-items: center;
  border-radius: solid black 10px;
  background-color: white;
  border: 1px;
  width: 200px;
  width: 100%;
  margin: auto;
}
button {
  display: flex;
  justify-items: flex-end;
  align-self: flex-end;
  justify-items: flex-end;
  height: 20px;
  width: 70px;
  background: rgb(47, 142, 231);
  color: white;
}
form {
  display: flex;
  justify-items: center;
  align-self: center;
  justify-items: center;
  background-color: white;
  border: 1px;
  height: 200px;
  width: 200px;
  margin: auto;
  flex-direction: column;
  border-radius: 8px;
  border: 0.5px solid;
  padding: 40px;
}
</style>
