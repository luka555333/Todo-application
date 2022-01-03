<template>
  <div id="app">
    <div class="container">
      <div class="row aligning">
        <div class="col-12">
         
          <p>MOJA TODO APLIKACIJA</p>
          <div class="input-table">
          <input class="todo-input" type="text" @keyup.enter="pushGrocery" v-model="input" />
    <button class="btn btn-primary" @click="pushGrocery">Submit</button>
    </div>
    </div>
    </div>

    <div class="row">
      <div class="col-12 centering">
        <div class="col-12">
    <todoItem 
     v-for="item in groceryList" 
    :key="item.text"
    :todo="item"
    @update-item="deleteItem"
    @completed-item="completedItem"
    />
      </div>
     </div>
    </div>
    
    
    </div>
  </div>
</template>

<script>

import todoItem from './components/todoItem.vue';
export default {
  name: 'App',
  components: {
    todoItem
  },
  data () {
     return{
     checked: [],
     groceryList:[],
     input: '',
    }
  },
  created(){
  console.log("app is created");
  },
  methods: {
    pushGrocery(){
      if(!this.input){
        return;
      }
      this.groceryList.push({text: this.input, completed: false, message: 'Upisao si ovu obavezu' + ' ' + new Date().toLocaleString()});
      this.input='';
     
    },
    deleteItem(todo){
      const index = this.groceryList.indexOf(todo);
     this.groceryList.splice(index, 1);
    },
    completedItem(todo){
     todo.completed = !todo.completed
    },
  },
  mounted(){
   if(localStorage.groceryList){
     this.groceryList = JSON.parse(localStorage.groceryList);
   }
   
   
  },
  watch:{
    groceryList: {
      deep: true,
      handler(newTodo){
         localStorage.groceryList = JSON.stringify(newTodo);
      },
    },
  },

}
</script>

<style>
@import'~bootstrap/dist/css/bootstrap.css';
.active{
  color: blue;
}
li{
  list-style: none;
  font-size: 20px;
  text-align: left;
  color: red;
}
.container{
  margin-top: 50px;
}
.row{
  justify-content: center;
  text-align:center;
}
.todo-input{
  font-size: 19px;
  vertical-align: middle;
  width:40%;
}
.btn{
  border: none;
  font-size: 15px;
   border-radius: 0px;
   color: white;
}
p{
  font-weight: 500;
  font-size: 20px;
}
.centering{
  padding: 0;
  width:43%;
}
.todo-checkbox{
  width:20px;
  height: 30px;
}
svg{
  color: red;
}
.icons{
  font-size: 1.2em;
  
}
.is-completed{
  text-decoration: line-through;
}
.todo-container{
  border: 1px solid black;
  justify-content: center;
  align-items: center;
}
.color-change{
  color:green;
  font-weight: 800;
}
input[type="text"]{
  outline: none;
}
input[type="text"]:focus{
 border: 1px solid blue;
}
.sizing{
  font-size:10px;
  text-align: left;
}
</style>