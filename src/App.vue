<template>
  <div>
    <TodoList />
  </div>
</template>
<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList,
  },
};
</script>
<style>
html {
  min-width:300px;
  background:#fafafa;
}
* {
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  user-select: none;
}
#inner {
  max-width:480px;
  margin:0 auto;
  background:white;
  box-shadow:0 1rem 2rem rgba(0,0,0,0.25), 0 0 0.5rem rgba(0,0,0,0.25);
  border:1rem solid #eee;
  border-radius: 2rem;
  padding:2rem;
  box-sizing: border-box;
}
  h2, h3 {
    border-bottom:1px solid black;
    text-align: center;
  }
  h3 span {
    color:#aaa;
    font-size:1rem;
  }
  ul {
    list-style: none;
    margin:0; 
    padding:0;
  }
  ul.complete li {
    text-decoration: line-through;
  }
  li {
    padding:0.25rem 0;
    cursor:pointer;
  }
  li:hover {
    background:rgba(255,255,0,0.25);
  }
  .grid {
    display:grid;
    grid-template-columns: 78% 22%;
  }
  .grid input, .grid button {
    width:100%;
    cursor:pointer;
    height:2rem;
    box-sizing: border-box;
    padding:0 0.5rem;
  }
  .clearAll {
    font-size:0.8rem;
    text-align:center;
    display:block;
    margin:0 auto;
    width:50%;
    padding:0.25rem;
    cursor:pointer;
  }
  .clearAll:hover {
    background:#eee;
  }
</style>