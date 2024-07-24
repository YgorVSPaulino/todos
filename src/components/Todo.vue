<template>
  <div class="flex flex-col items-center p-10">
    <h3 class="text-2xl font-bold mb-4">Todo List</h3>
    <div class="m-10 w-full max-w-md">
      <ul class="list-decimal ml-5">
        <li v-for="todo in todos" :key="todo.id" class="mb-2">
          <span :class="{ done: todo.done }" @click="todo.done = !todo.done">{{
            todo.text
          }}</span>
        </li>
      </ul>
    </div>
    <button
      class="bg-red-500 text-white p-2 rounded"
      @click="limparTarefas"
      v-if="todos.length">
      Limpar
    </button>
    <div class="block mt-5">
      <input
        type="text"
        placeholder="Digite sua Tarefa..."
        class="p-2 border rounded"
        v-model="newTodos.text" />
      <button
        class="ml-3 bg-blue-500 text-white p-2 rounded"
        @click="addNovaTarefa()">
        Adicionar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todos: [
        { text: "Primeiro item", done: true, id: 1 },
        { text: "Segundo", done: false, id: 2 },
      ],
      newTodos: {},
      limpar: [],
    };
  },
  created() {
    this.todos = localStorage.getItem('todos') ? JSON.parse(localStorage.getItem('todos')) : this.todos
  },
  updated() {
    localStorage.setItem("todos", JSON.stringify(this.todos))
    console.log("Chegamos aqui");
  },
  methods: {
    addNovaTarefa() {
      if (this.newTodos.text) {
        this.todos.push(this.newTodos);
        this.newTodos = {
          done: false,
        };
        this.salvarTarefas();
        
      } else {
        alert("Você precisa Preencher o campo");
      }
    },
    limparTarefas() {
      this.todos = [];
    },
    salvarTarefas() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
