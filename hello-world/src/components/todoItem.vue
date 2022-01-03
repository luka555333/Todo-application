<template>
   <div class="row mt-2">
     <div class="col-8 todo-container">
       <li :class="[{'is-completed': todo.completed}, {'color-change': todo.completed}]">
         {{ todo.text }}
        
         </li>
          <div class="text-muted sizing">{{todo.message}}</div>
    </div>
     <div class="col-2 todo-container d-flex">
       <span class="icons" @click="deleteItem"><i class="fas fa-trash icons"></i></span>
    </div>
    <div class="col-2 todo-container d-flex">
      <input class="todo-checkbox" v-if="completedItem" type="checkbox" @click="completedItem" />
    </div>
   </div>
</template>

<script>
    export default {
        name:'todoItem',
        props: {
              todo:{
                type: Object,
              },
              
        },
        methods: {
            deleteItem(){
             this.$emit('update-item', this.todo)
           },
           completedItem(){
               this.$emit('completed-item', this.todo)
           },
        },
    }
</script>
