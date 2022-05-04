<template>
  <img alt="Vue logo" src="./assets/head.jpg" class="head-img">
  <h1>Let's get all your tasks on the GO!</h1>

  <hr>

  <form action="" @submit.prevent="addNewTodo" >
    <label for="add-todo">New Todo Items</label>
    <div id="flex-1">
      <input type="text" name="" id="add-todo" v-model=newTodo>
      <button id="add" >Add Todo</button>
    </div>
  </form>
  
  <div id="flex-2">
      <button @click="markAsDone" id="done" v-if="togg"><img src="./assets/check.svg" alt=""><span>Mark All As Done</span></button>
      <button @click="unMarkAsDone" id="done" v-if="togg2"><img src="./assets/check.svg" alt=""><span>Unmark All</span></button>
    <button @click="removeAllTodo" id="remove"><img src="./assets/trash.svg" alt="" id="trash"><span>Delete All Todo</span></button>
  </div>

     <center>
        <div v-for="todo in todos" :key="todo.id" id="todo">
      <h3 :class="{done: todo.done}"  id="content">{{todo.content}}</h3>
      <div id="checkbox"><input type="checkbox" @click="toggleDone(todo,index)" id="checkbox-btn"></div>
      <div @click="removeTodo(index)" id="delete"><img src="./assets/trash.svg" alt="" id="trash-2"></div>
     </div>
     </center>

</template>
 
<script>
import {ref} from "vue";
export default { 
  name: 'App',
  setup(){
    const newTodo = ref('');
    const markAll = ref("Mark All As Done");
    const todos = ref([]);
    const togg = true;
    const togg2 = false;
    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function addNewTodo(){
    if(newTodo.value != ''){
      todos.value.push({
       id:Date.now(),
       done:false,
       content: newTodo.value,
     });
    }
    newTodo.value= "";
    }

    function markAsDone(){
    if(this.togg=true){
        todos.value.forEach((todo) => {
        todo.done = true;
         });

         this.togg = false;
         this.togg2 = true;
     }
    }

   function unMarkAsDone(){
      todos.value.forEach((todo) => {
        todo.done= false;
      });

      this.togg=true;
      this.togg2 = false;

   }

    function removeTodo(index){
      todos.value.splice(index,1)
    }
    function removeAllTodo(todo){
      todos.value=[]
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAsDone,
      unMarkAsDone,
      markAll,
      togg,
      togg2,
      removeAllTodo,
    }
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #097ff5;
  display:block;
  margin: 0 auto;
  margin-top:60px;
  padding: 1rem 0.5rem;
  border-radius:10px;
  width:100vw;
  border:1px solid rgba(255, 255, 255, 0.267);
  background: rgba(255, 255, 255, 0.208);
}
body{
  background: rgb(255, 255, 255);
}
form{
  min-width:50vw;
  max-width: 400px;
  margin:0 auto;
}
input,label, button{
  display:block;
  margin:1rem auto;
  width:100%;
}
.done{
  text-decoration-line: line-through;
  text-decoration-style: double;
  text-decoration-color: black;
  color:white;
}
input[type=text]{
  padding: 0.5rem;
  border:none;
  border-radius: 5px;
  margin-right:10px;
  margin-left:10px;
  width:70%;
  font-size: 20px;
  color:white;
  background: crimson;
}
input:focus{
   outline:none;
}
button{
  width: 10rem;
  border:none;
  color:white;
  padding:0.5rem;
}
ul{
  list-style-type: none;
  width:100%;
}
li{
  text-transform: uppercase;
  font-size: 11px;
}
img{
  height:20px;
}
.head-img{
  height: 200px;
}

#flex-1, #flex-2{
  display:flex;
  margin:5px auto;
  justify-content: center;
  max-width: 400px;
}

#remove{
  background: #eee;
  color:red;
  font-weight:700;
  display:flex;
  align-items: center;
  border: 1px red solid;
  border-radius: 10px;
}
#remove:hover{
  background: red;
  color:#fff 
}
#remove img{
  border: none;
  margin-right: 5px;
  padding: 2px; 
}

#remove:hover img{
  filter: grayscale(1) invert(1) brightness(100)
}

#add{
  background: rgb(3, 170, 92);
  width: 25%;
  border-radius:5px;
}
#done{
  background: rgb(255, 255, 255);
  display:flex;
  align-items: center;
  border: 1px rgb(58, 170, 92) solid;
  color:rgb(58, 170, 92);
  border-radius: 10px;
}
#done img{
  border: 2px rgb(58, 170, 92) solid;
  margin-right: 5px;
  border-radius: 50%;
  padding: 2px; 
}
#todo{
  display:flex;
  margin:5px auto;
  width: 94%;
  background: crimson;
  align-items: center;
  height: 30px;
  border-radius: 5px;
}
#content{
  width:80%;
  text-align: left;
  overflow: hidden;
  margin-left: 0.5rem;
  white-space: nowrap;
  color: white;
  font-weight:400;
  padding: 3px 2px 3px 4px;
}
#checkbox, #delete{
  width:10%;
  height:20px;
  margin: 5px;
  background: none;
}
#checkbox-btn{
  height: 20px;
  margin: 0 5px;
  accent-color:rgb(3, 148, 88);
}
#trash-2{
height:20px;
margin: 0 5px;
filter: grayscale(100%) invert(100%);
}
@media only screen and (min-width:600px) {
  #app{
    width:600px;
  }
}
</style>
