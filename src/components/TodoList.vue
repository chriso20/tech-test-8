<template>
    <h2>Todo List</h2>
  <div id="inner">
    <div class="grid">
        <div class="left">
            <input type="text" v-model="newTodo" placeholder="Add new todo item">
        </div>
        <div class="right">
            <button @click="addTodo">Add</button>
        </div>
    </div>

    <h3>To Do <span>({{ incompleteTodos.length }} items)</span></h3>
    <ul class="incomplete">
      <li v-for="todo in incompleteTodos" :key="todo.id">
        <TodoItem :todo="todo" @toggleCompleted="toggleCompleted" />
      </li>
    </ul>
    <h3>Completed <span>({{ completedTodos.length }} items)</span></h3>
    <ul class="complete">
      <li v-for="todo in completedTodos" :key="todo.id">
        <TodoItem :todo="todo" @toggleCompleted="toggleCompleted" />
      </li>
    </ul>
    <hr>
    <a class="clearAll" @click="clearAll">Clear All Items</a>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  data() {
    return {
      todos: [],
      newTodo: '',
    };
  },
  mounted() {
    // get the existing todo items from local storage, or set a default (incredibly humorous) array
    if(localStorage.getItem('todos') !== null){
        this.todos =  JSON.parse(localStorage.getItem('todos'));
    }else{
        this.todos = [
            {id:2, title:"Make Pulse say 'yep, that's a todo list app'", completed:false},
            {id:1, title:"Complete a basic todo list app", completed:true}
        ];

    }
  },
  watch: {
    todos: {
        handler(todos) {
            localStorage.setItem('todos', JSON.stringify(todos));
        },
        deep: true,
    },
  },
  computed: {
    completedTodos() {
      // just get the todo items which are "completed"
      return this.todos.filter(todo => todo.completed);
    },
    incompleteTodos() {
        // guess what this does!
        return this.todos.filter(todo => !todo.completed);
    },
  },
  methods: {
    addTodo() {
        // Check if the todo item exists already
        if (this.todos.some(todo => todo.title === this.newTodo)) {
            alert('This todo item already exists!');
            return;
        }

        //get a new unique ID
        const newId = this.todos.length + 1;

        // add the new todo item to the array
        this.todos.push({ id: newId, title: this.newTodo, completed: false });

        // reset the input text box value
        this.newTodo = '';
    },
    toggleCompleted(id) {
      // get this todo item
      const todo = this.todos.find(todo => todo.id === id);

      // toggle its status
      todo.completed = !todo.completed;
    },
    clearAll(){
        this.todos = [];
    }
  },
};
</script>