<script setup lang="ts">
import {ref, reactive, watch} from 'vue'
import PlayLeft  from "../components/PlayLeft.vue";

const message = ref('class1')
const textValue = ref('')
const count = ref(0)
const count3 = ref(false)
const counter = reactive({
    counter: 0
})
function counterIncrement() {
    counter.counter++
    updateCount3()
}
function resetCounter(){
    counter.counter = 0
    updateCount3()
}

function updateCount3(){
    if(counter.counter==3){
        count3.value = true
        return
    }
    count3.value = false
}

// -------------------- List TOdos ----------------------
let id = 0
const newTodo = ref('')
const todos = ref([
    {key:id++, text: 'Hello', done:true},
    {key:id++, text: 'There', done:false}
    ])
function addNewTodo(){
    todos.value.push({key: id++, text: newTodo.value, done:false})
    newTodo.value = ''
}

function removeTodo(todo: { key: number; text: string; done: boolean; }){
    todos.value =  todos.value.filter((e)=> e != todo);
}
// --------------- Watch ---------------------
watch(counter,(newCount)=>{
    console.log(`new count value ${newCount.counter}`);
    
})
function countIncrement(){
    count.value++
}
const count2 = ref(0)
function decrement() {
    count2.value--
}
</script>

<template>
      <!-- <PlayLeft v-bind:message='Hello message'/> -->

    <main>
      <!-- <h1 :class="message">{{ message }}</h1> -->
      <h1>Counter : {{ counter.counter }}</h1>
      <button v-on:click="resetCounter">Reset Counter</button>
      <button v-on:click="counterIncrement">Increment Counter</button>

      <span>counter new {{ count }}</span>

      <button @click="decrement">Decrement</button>
      <br>
      <input v-model="textValue" placeholder="Type Here">
      <p >{{ textValue }}</p>
      <br>
      <h1 v-if="count3">count == 3</h1>
      <h1 v-else>Count != 3</h1>
      <br>
      <h1 id="hoverList">List Objects</h1>
      <input v-model="newTodo" placeholder="New Todo">
      <button @click="addNewTodo">Add</button>
      <br>
      <ul>
        <li v-for="todo in todos" v-bind:key="todo.key">
            <input type="checkbox" v-model="todo.done">
            <span :class="{done: todo.done}">{{ todo.text }}</span>
            <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>
      <br>
      <p>count : {{ count }}</p>
      <button @click="countIncrement">Increment only count</button>
  </main>

</template>

<style>
#hoverList:hover{
    background-color: pink;
    color: red;
}
main{
    height: 100vh;
}

.class1{
    color:red;
}

.done{
    text-decoration: line-through;
}
</style>
