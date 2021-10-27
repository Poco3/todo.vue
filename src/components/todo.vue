<template>
  <div>
    <h1>ToDoリスト</h1>
    <input type="radio" value="all" v-model="select" />
    <label>すべて</label>
    <input type="radio" value="work" v-model="select" />
    <label>作業中</label>
    <input type="radio" value="done" v-model="select" />
    <label>完了</label>
    <table>
      <thead>
        <tr class="test">
          <th>ID</th>
          <th>コメント</th>
          <th>状態</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, i) in computedTodos" :key="i">
          <td>{{ todo.id }}</td>
          <td>{{ todo.comment }}</td>
          <td>
            <button @click="changeTodo(todo)">{{ todo.status }}</button>
          </td>
          <td>
            <button @click="deleteTodo(i)">削除</button>
          </td>
        </tr>
      </tbody>
    </table>

    <h2>新規タスクの追加</h2>
    <input type="text" v-model="texttodo" />
    <button @click="addoTodo">追加</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      texttodo: "",
      todos: [],
      select: "all",
    };
  },
  methods: {
    addoTodo() {
      if (this.texttodo == "") return;
      const todo = {
        id: this.todos.length,
        comment: this.texttodo,
        status: "作業中",
      };
      this.todos.push(todo);
      this.texttodo = "";
    },
    deleteTodo(i) {
      this.todos.splice(i, 1);
      this.todos.reduce((index, todo) => (todo.id = index + 1), -1);
    },
    changeTodo(todo) {
      if (todo.status === "作業中") {
        todo.status = "完了";
      } else {
        todo.status = "作業中";
      }
    },
  },
  computed: {
    computedTodos() {
      if (this.select === "work") {
        return this.todos.filter((todo) => todo.status === "作業中");
      } else if (this.select === "done") {
        return this.todos.filter((todo) => todo.status === "完了");
      } else {
        return this.todos;
      }
    },
  },
};
</script>
<style>
div {
  text-align: left;
}
</style>
