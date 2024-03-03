<template>
  <div class="">
    <div
      class="w-full h-screen flex flex-col justify-center items-center p-2 rounded-xl"
    >
      <div class="inputbox bg-[#3b3b3b] p-2 rounded-xl">
        <input type="text" class="outline-none" />
        <button @click="addToData()" class="addbtn bg-green-500 px-4 py-2 rounded-xl">ADD</button>
      </div>
      <div class="">
        <ul class="">
          <Todo
            class="py-2"
            v-for="(todo, index) in todos"
            :key="index"
            :todoItem="todo.todoString"
            @on-delete = "deleteData(todo)"
            @on-edit = "editData(Data, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  data() {
    return {
      todos: [
        { todoString: "Taking bath at 9:00 am", completed: false },
        { todoString: "Taking Lunch at 10:00 am", completed: false },
        { todoString: "Taking office at 11:00 am", completed: false },
        { todoString: "Taking leave at 7:00 pm", completed: false },
      ],
    };
  },
  components: {
    Todo,
  },
  mounted() {
    this.fetchData();
    this.saveData();
  },
  //   watch() {},
  methods: {
    fetchData() {
      const storedData = localStorage.getItem("todos");
      if (storedData) {
        this.todos = JSON.parse(storedData);
      }
    },
    saveData() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    addToData(newData) {
      this.todos.push({
        todoString: newData,
        completed: false,
      });
    },
    deleteData(deleteItem) {
      this.todos = this.todos.filter((todo) => todo !== deleteItem);
    },
    editData(Data, newData) {
      Data.todoString = newData;
    },
    clearAllData() {
      localStorage.removeItem("todos");
    },
  },
};
</script>

<style></style>
