<template>
  <div id="app" class="container">
 <Header/>
 <br>
 <TodoList/>
  </div>
</template>

<script>
import Header from './components/Header';
import TodoList from './components/TodoList';


export default {
  name: 'App',
  components: {
    Header,
    TodoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}

.container {
  box-sizing: border-box;
  margin-top: 5px;
}
</style>
