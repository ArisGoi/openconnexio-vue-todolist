<template>
  <section class="TodoList">

    <div class="top-bar">
      <input 
        type="text" 
        v-model="newTodo" 
        v-on:keyup.enter="addTodo()" 
        placeholder="Scrivi un titolo"
      >
      <button @click="addTodo()">+</button>
    </div>

    <div class="list-todo">
      <h3>Da Fare</h3>

      <ul v-if="todos.length > 0">

          <li v-for="(todo, index) in todos" :key="todo.index" :style="todo.check ? 'display: none' : null">
            
            <div class="checkbox" @click="doToggle(index)"></div>
            <p>{{todo.title}}</p>

            <div class="actions">
              <i class="far fa-clone" @click="cloneTodo(index)"></i>
              <i class="far fa-edit" @click="editTodo(index)"></i>
              <i class="fas fa-times" @click="removeTodo(index)"></i>
            </div>

          </li>

      </ul>

    </div>

    <div class="list-completed">
      <h3>Completati</h3>

      <ul v-if="todos.length > 0">

          <li v-for="(todo, index) in todos" :key="todo.index" :style="!todo.check ? 'display: none' : null">

            <div class="checkbox checked" @click="doToggle(todo)"></div>
            <p>{{todo.title}}</p>

            <div class="actions">
              <i class="fas fa-times" @click="removeTodo(index)"></i>
            </div>

          </li>

      </ul>
      
    </div>

  </section>
</template>

<script>
export default {
  name: 'TodoList',
  data(){
    return{
      // Input nuovo todo
      newTodo: null,

      // Lista todos
      todos: [
        {
          title: "Lavare i piatti",
          check: false,
        },
        {
          title: "Fare la spesa",
          check: false,
        },
        {
          title: "Inviare Curriculum",
          check: false,
        }
      ]
    }
  },
  methods: {
    // addTodo() -> Pusha un todo alla lista
    addTodo(){
      if(this.newTodo != null && this.newTodo != ''){
        this.todos.push(
            {
                title: this.newTodo,
                check: false,
            }
        );
        this.newTodo = "";
      }
    },

    // cloneTodo(index) -> Pusha in lista un clone del todo con (index) selezionato
    cloneTodo(index){
      const {title, check} = this.todos[index];
      this.todos.push(
        {
          title: title,
          check: check,
        }
      )
    },

    // editTodo(index) -> Usa un prompt per modificare il title del todo con (index) selezionato
    editTodo(index){
      let change = prompt('Inserisci il nuovo titolo');
      if(change != null && change != ''){
        this.todos[index].title = change;
      }
    },

    // removeTodo(index) -> rimuove il todo selezionato
    removeTodo(index){
      this.todos.splice(index, 1)
    },

    // toggleTodo(index) -> toggle sullo stato di check del todo selezionato
    doToggle(index){
      if(this.todos[index].check){
        this.todos[index].check = false
      } else {
        this.todos[index].check = true
      }
    },
  }
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/style.scss';

.TodoList{
  width: 100%;
  border: 2px solid black;
}

.checkbox{
  height: 20px;
  width: 20px;
  background-color: lightgray;

  &.checked{
    background-color: green;
    position: relative;
    &::after{
      content: "\f00c";
      font-weight: 900;
      font-family: "Font Awesome 5 Free";
      color: white;
      font-size: 15px;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
}

.top-bar{
  height: 60px;
  @include flex-center;
  border-bottom: 2px solid black;

  input, button{
    height: 30px;
    padding: 5px;
    border: 1px solid black;
    border-radius: 0;
  }
  button{
    @include flex-center;
    width: 30px;
    border-left: none;
    font-size: 20px;
    font-weight: 900;
  }
}

[class^="list-"]{
  h3{
    margin: 10px 10px 0 10px;
  }

  ul{
    width: 100%;
    padding: 20px;

    li{
      margin-bottom: 20px;
      @include flex-center;
      justify-content: flex-start;
      position: relative;
      &::after{
        content: '';
        height: 1px;
        width: 100%;
        background-color: lightgray;
        position: absolute;
        bottom: -10px;
        left: 0;
      }

      p{
        flex-grow: 1;
      }

      .checkbox{
        margin-right: 10px;
      }

      .actions i{
        margin-left: 10px;
      }
    }

  }
}



</style>