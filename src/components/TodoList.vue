<template>
<div class="container">
      <input type="text" class="todo-input" 
      placeholder="Add a new To Do" v-model="newTodo" @keyup.enter="addTodo">
      <div v-for="(todo, index ) in todos" :key="todo.id" class="todo-item">
          
          <div class="todo-item-left">

              <input type="checkbox" v-model="todo.completed">
              <div v-if="!todo.editing" @dblclick="editTodo(todo)" 
              class="todo-item-label" :class="{ completed : todo.completed}">{{ todo.title }}</div>
              
              <input v-else class="todo-item-edit" type="text" 
              v-model="todo.title" @blur="doneEdit(todo)" 
              @keyup.enter="doneEdit(todo)" @keyup.escape="cancelEdit(todo)" v-focus>
          </div>
      
      <div class="remove-item" @click="removeTodo(index)">
          &times;
      </div> 
  </div>

  <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos">
      Check all</label></div>

  <div> {{ remaining }} items left </div>
  </div>


  <div><h6>Note: double click on existing to-do for editing</h6></div>
</div>
</template>


<script>
export default {
name: 'to-do-vue',
  data () {
    return {
      newTodo: '',
      idForTodo: 4,
      beforeEditCache: '',
      filter: 'all',
      todos: [
          {
              'id': 1,
              'title': 'Task one',
              'completed': false,
              'editing': false,
          },
          {
              'id': 2,
              'title': 'Task two',
              'completed': false,
              'editing': false,
          }, 
          
          {
              'id': 3,
              'title': 'Task three',
              'completed': false,
              'editing': false,
          }, 
      ]
    }
  },
computed: {
      remaining() {
      return this.todos.filter(todo => !todo.completed).length
      },
      anyRemaining() {
        return this.remaining != 0

      }
  },    
directives: {
      focus: {
          inserted: function (el) {
              el.focus() 
          }
      }
  },
methods: {
    addTodo() { 
          if(this.newTodo.trim().length == 0){
              return
          }
          this.todos.push({
              id:this.idForTodo,
              title: this.newTodo,
              completed: false,
          })
        this.newTodo = ''
        this.idForTodo++    
    },

    editTodo(todo){
        this.beforeEditCache = todo.title
        todo.editing = true
    },

    doneEdit(todo) { 
          if(todo.title.trim() == ''){
              todo.title = this.beforeEditCache
          } 
        todo.editing = false
    },

    cancelEdit(todo) {
        todo.title = this.beforeEditCache
        todo.editing = false
    },

    removeTodo(index) {
        this.todos.splice(index, 1)
    },
     checkAllTodos() {
        this.todos.forEach((todo) => todo.completed = event.target.checked)
    }
  }
}
</script>


<style>

.todo-input {
    width: 90%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 30px;
}

.todo-item {
    margin-bottom: 15px;
    display: flex; 
    align-items: center;
    justify-content: space-between;
}

.remove-item {
    cursor: pointer;
    margin-left:  14px;    
}

.todo-item-left {
    display: flex;
    align-items: center;
}

.todo-item-label {
    padding: 10px;
    border: 1px solid grey;
    margin-left: 14px;
}

.todo-item-edit {
    font-size: 24px;
    color: grey;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #3b3b3b;
    font-family: Avenir, Helvetica, Arial, sans-serif;
}

.completed {
    text-decoration: line-through;
    color: gray;
}

.extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 10px;
    border-top: 1px solid lightgray;
    padding-top: 14px;
    margin-bottom: 14px;
}
</style>

