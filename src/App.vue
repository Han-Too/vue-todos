<template>

  <div class="container" style="margin-top: 20px;">
    <div class="card text-start">
      <div class="card-body">
        <h3 class="card-title text-center mb-5">Simpel ToDo App</h3>
        <div class="row">
          <div class="col-10">
            <div class="mb-3">
              <input 
              @keyup.enter="add()"
              v-model="todo" type="text" 
              class="form-control" 
              />
            </div>
          </div>
          <div class="col">
            <button @click="add" class="btn btn-success">
              Add
            </button>
          </div>
        </div>
        <list :todos="todos" 
        @deletetodo="deletetodo"
        @donetodo="donetodo"
        />
        <small>
          Total : {{ totaltodo }}
        </small>
      </div>
    </div>
  </div>

</template>

<script>

import List from './components/List.vue';

export default {
  components: { List },
  mounted(){
    this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  data() {
    return {
      todo: "",
      todos: []
    }
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false
      });
      this.todo="";
      this.saveToLocalStorage(); 
    },
    deletetodo(todoIndex){
      this.todos = this.todos.filter(
        (item,index) => {
        if(index != todoIndex){
          return item
        }
      });
      this.saveToLocalStorage(); 
    },
    donetodo(todoIndex) {
      this.todos = this.todos.filter(
        (item,index) => {
          if(index == todoIndex ){
            item.isDone = true
          }

          if(item.isDone){
            item.isDone != item.isDone
          }

          return item;
        }
      );
      this.saveToLocalStorage(); 
    },
    saveToLocalStorage(){
      localStorage.setItem('todos',JSON.stringify(this.todos));
    }
  },
  computed:{
    totaltodo(){
      return this.todos.length;
    }
  }
}
</script>
