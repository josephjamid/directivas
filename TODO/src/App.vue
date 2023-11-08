<script setup>
import { ref } from 'vue';

let newTask = ref('')
let taskList =  ref([
{
name : 'estudiar',
done: true
},
{
  name:'comer',
  done: false
},
{
  name: 'dormir',
  done:false
}
])
 
function setDone(index){
  taskList.value[index].done = true
}


function addTask(){
  if(newTask.value.trim() === '') return
  taskList.value.push({
    name: newTask.value,
    done: false
  })
  newTask.value= '';

}
</script>

<template>
<div class="contenedor">
  <h1>Lista de tareas</h1>
  <p class="subtitle">{{ newTask }}</p>

  <div>
    <div class="task" :class="{done: task.done}" v-for=" (task, index) in taskList " :key="index"> {{ task.name }}<span @click="setDone(index)" class="button">x</span></div>
     
   
    
  </div>

  <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escriba su tarea">
  <p v-show="newTask != ''" class="help">Presiona enter para agregrar la tarea</p>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
.contenedor{
  padding: 6px 12px;
  background-color: #015958;
 font-family: 'Roboto Mono', monospace;
 color: aliceblue;
  border-radius: 6px;
  max-width: 420px;
  margin: 0 auto;
  
}
h1{
  text-transform: uppercase;
  font-size: 20px;
  text-align: center;
  margin: 0;
  margin-top: 12px;
}
.subtitle{
  margin: 0;
  margin-bottom: 15px;
  text-align: center;
  opacity: 0.6;
}
.task{
  display: flex;
  justify-content: space-between;
  background-color: #0FC2C0;
  border-radius: 3px;
  margin-bottom: 1px;
  padding: 2px 2px 1px 6px;
}
.task:hover{
  background-color: #023535;
}
.button{
  background-color: #015958;
  display: inline-block;
  padding: 0 6px;
  border-radius: 3px;
}
.button:hover{
  cursor: pointer;
}
input{
  border: none;
  border-radius: 3px;
  padding: 2px 6px;
  outline: none;
  /*width: calc(100% - 12px );*/
  box-sizing: border-box;
  width: 100%;

}
input::placeholder{
  opacity: 0.4;
}
.help{
  font-size: 8px;
  opacity: 0.7;
  margin: 0;
}

</style>
