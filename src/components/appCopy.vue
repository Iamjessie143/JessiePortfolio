<template>
  <div class="container">
    <div class="title"><h1>Todo App</h1></div>
    <div class="actions">
      <form @submit="addTask">
        <input type="text" placeholder="Add Task" v-model="task" required>
        <button type="submit">Add</button>
        <input type="text" class="search" placeholder="Search Task">
      </form>
    </div>
    <div class="tasks">
      <div class="task-items" v-for="todo in todos" :key="todo.id">
        <p :id="todo.id" >{{ todo.details }}</p>
        <button class="done-btn" @click="doneTask(todo.id)">Done</button>
        <button class="remove-btn" @click="removeTask(todo.id)">Remove</button>
      </div>
      <button  v-if="showButton" class="clear-btn" @click="clearTask()">Clear ALL task</button>
    </div>
  </div>
  
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
export default {
  data(){
    return{
      task:'',
      todos:[],
      isDone:false,
      showButton:false,


    }
  },
  methods:{
    addTask(e){
      e.preventDefault();
      const newTask = {
        id:'a'+uuidv4(),
        details:this.task,
        status:false,
        isDone:false
      }
      
      this.todos.unshift(newTask);
      this.task=''
      this.showButton=true
      this.isDone=false
      console.log(newTask.id)

    },
    removeTask(id){
      const index = this.todos.findIndex(todo => todo.id == id);
      if (this.todos.length === 1) {
        this.todos=[]
        this.showButton=false
        console.log(this.todos.length)
      }else{
        console.log(this.todos.length+ " sdsadas")
        this.todos.splice(index, 1);
        
      }
      
    },
   
    doneTask(id) {
      const index = this.todos.findIndex(todo => todo.id === id);
      if (index !== -1) {
          console.log(id);
          // document.querySelector(`#${id}`).style.textDecoration="line-through"
          var data = document.querySelector(`#${id}`)
          data.style.textDecoration = "line-through"
      }
          
      
    },  
    clearTask(){
      if(this.todos.length != -1){
        // console.log(this.todos.length)
        this.todos = []
        this.showButton = false
      }

    }
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
.container{
  border:5px solid;
  border-radius: 5px;
  width: 500px;
  padding:50px;
  margin:0 auto;
  text-align: center;
  background-color:#F08080 ;
}
.task-items{
  display: flex;
  padding:5px;
  width: 270px;
  border:1px solid #666;
  margin: 5px;
  align-items: center;
  border-radius: 5px;
}
.task-items:hover{
background-color: #ccc;
cursor: pointer;
}
.remove-btn{
  background-color: red;
  color:#fff;
  width: auto;
  height: auto;
  font-size: 14px;
  padding:5px;
  margin-right: 10px;
  cursor: pointer;
  border:1px solid;
  border-radius: 5px;
}
.done-btn{
  background-color: blue;
  color:#fff;
  width: auto;
  height: auto;
  font-size: 14px;
  padding:5px;
  cursor: pointer;
  border:1px solid;
  border-radius: 5px;
  margin-left: auto;
}
.clear-btn{
  background-color: black;
  color:#fff;
  width: auto;
  height: auto;
  font-size: 14px;
  padding:5px;
  cursor: pointer;
  border:1px solid;
  border-radius: 5px;
  margin-left: auto;
}
.strikethrough {
  text-decoration: line-through;
}
.search{
  margin-left: 50px;
}

</style>
