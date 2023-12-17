<template>
  <div class="container">
    <br>
    <div class="title"><h1>Todo App</h1></div>
      <form @submit="addTask">
        <input type="text" placeholder="Add Task" v-model="task" required>
        <button  class="submit" type="submit">Add</button>
        <input type="text" class="search" placeholder="Search Task">
  </form>
  
      <br>
      <div class="task-items" v-for="todo in todos" :key="todo.id">
        <p :id="todo.id" >{{ todo.details }}</p>
        <button class="done-btn" @click="doneTask(todo.id)">Done</button>
        <button class="remove-btn" @click="removeTask(todo.id)">Remove</button>
      </div>
      <br>
      <br>
      <br>
      <br>
      <button  v-if="showButton" class="clear-btn" @click="clearTask()">Clear ALL task</button>
    </div>
    <br>
  
  
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
/* General styles */

/* Style for the container */
.container {
  margin-left: 20rem;
  width: 600px;
  height: 400px;
  text-align: center;
  background-color: #2ecc71;
  border-radius: 10px;
  border: 3px solid black;
}
.container :hover{
  color: skyblue;
}
/* Style for the title */
.title {
  margin-bottom: 20px;
  color: #3498db; /* Blue color */
  
}

/* Style for the form container */
.inputs {
  margin-bottom: 20px;
}

/* Style for the form */
form {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 30rem;
  margin-left: 50px;
}

/* Style for the add task input */
input[type="text"] {
  padding: 10px;
  width: 50%;
  box-sizing: border-box;
  margin-bottom: 10px;
  border: 1px solid #3498db; /* Blue border */
  border-radius: 5px;
}

/* Style for the submit button */
.submit {
  flex: 1;
  margin: 0 5px;
  width: 50px;
  padding: 10px;
  background-color: blue; /* Green color */
  color: #fff; /* White text color */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s; /* Smooth transition for the background color */
}

/* Hover effect for the submit button */
.submit:hover {
  background-color: #27ae60; /* Darker green color on hover */
}

/* Style for the search input */
.search {
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  margin-right: 0;
  border: 1px solid #e74c3c; /* Red border */
  border-radius: 5px;
}

/* Style for the task items container */
.task-items {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f9f9f9;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 10px;
  width: 30rem;
  margin-left: 3rem;
}

/* Style for the Done and Remove buttons */
.done-btn{
  margin-top: 5px;
  padding: 8px;
  background-color: blue; /* Orange color */
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  width: 80px;
  margin-left: 20rem;
  transition: background-color 0.3s;
}
.remove-btn {
  margin-top: 5px;
  padding: 8px;
  background-color: red; /* Orange color */
  color: #fff;
  border: none;
  border-radius: 5px;
  width: 80px;
  cursor: pointer;
  transition: background-color 0.3s; /* Smooth transition for the background color */
}

/* Hover effect for the Done and Remove buttons */
.done-btn:hover,
.remove-btn:hover {
  background-color: #d35400; /* Darker orange color on hover */
}

/* Style for the Clear All button */
.clear-btn {
  width: 50%;
  margin-top: 10px;
  padding: 10px;
  background-color: red; /* Red color */
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s; /* Smooth transition for the background color */
}

/* Hover effect for the Clear All button */
.clear-btn:hover {
  background-color: #a93226; /* Darker red color on hover */
}


</style>
