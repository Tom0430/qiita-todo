<template>
  <div v-if="user">
    <p>{{user.name}}</p>
    <AddTodo @submit="addTodo" />
    <TodoList :todos="user.todos" />
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo";
import TodoList from "@/components/TodoList";
import axios from "@/plugins/axios";
import routerGuard from "@/middleware/routerGuard"


export default {
  components: {
    AddTodo,
    TodoList
  },
  computed: {
    user() {
      return this.$store.state.currentUser;
    }
  },
  methods: {
    async addTodo(todo) {
      const { data } = await axios.post("/v1/todos", { todo });
      this.$store.commit("setUser", {
        ...this.user,
        todos: [...this.user.todos, data]
      });
    }
  },
  middleware: "routerGuard"
  // async fetch({ store, redirect }) {
  //   console.log("www")
  //   await store.watch(
  //     state => state.currentUser,
  //     (newUser, oldUser) => {
  //       if (!newUser) {
  //         return redirect("/login");
  //       }
  //     }
  //   );
  // },
};
</script>

<style>
</style>