<template>
  <nav class="navbar">
    <img src="./assets/logo.svg" width="50" />
    <div class="brand">Todo List App</div>
  </nav>
  <main class="container">
    <Alert
      message="Todo title is required"
      :show="showAlert"
      @close="showAlert = false"

    ></Alert>
    <section>
      <form class="add-todo-form">
        <input v-model="todoTitle" type="text" placeholder="Todo Title" />
        <div>
          <button @click.prevent="addTodo">Add Todo</button>
        </div>
      </form>
    </section>
    <section>
      <div v-for="(todo, i) in todos" class="todo" :key="todo.id">
        <p>{{ todo.title }}</p>
        <div>
          <button @click="removeTodo(i)" class="remove-todo-btn">
            &times;
          </button>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import Alert from "./components/Alert.vue";

const component = {
  components: {
    Alert,
  },
  data() {
    return {
      todoTitle: "",
      todos: [],
      showAlert: false,
    };
  },

  methods: {
    updateTitle(e) {
      this.todoTitle = e.target.value;
      console.log(this.todoTitle);
    },
    addTodo(e) {
      if (this.todoTitle === "") {
        this.showAlert = true;
      } else {
        this.todos.push({
          title: this.todoTitle,
          id: Math.floor(Math.random() * 1000),
        });
      }
    },
    removeTodo(i) {
      this.todos.splice(i, 1);
    },
  },
};

export default component;
</script>

<style scoped>
.navbar {
  display: flex;
  background: var(--navbar-color);
  align-items: center;
  padding: 20px;
  margin-bottom: 30px;
}

.brand {
  font-size: 2rem;
}

.add-todo-form {
  display: flex;
  justify-content: space-between;
}

.add-todo-form input {
  width: 80%;
  border: solid 2px var(--accent-color);
}

.add-todo-form button {
  background-color: var(--accent-color);
  color: var(--text-color);
  border: none;
  height: 50px;
}

.todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--accent-color);
  margin-top: 30px;
  padding: 0 20px 0 20px;
  border-radius: 10px;
}

.remove-todo-btn {
  border-radius: 50%;
  border: none;
  height: 40px;
  width: 40px;
  font-size: 30px;
  color: var(--text-color);
  background: var(--danger-color);
  cursor: pointer;
}
</style>
