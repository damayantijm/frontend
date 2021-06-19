<template>
  <div>
    <!-- Budi {{ nilai }} {{ jk }}
    <button @click="nilai++"> Click Me </button>
    <button @click="gantiKelamin"> Click Here </button>
    <input v-model="nilai"/> -->

    <h1>Belajar Todo List</h1>
    <ul>
      <li v-for="item in todos" :key="item.id">{{ item.deskripsi }} <button @click="hapus(item.id)">X</button></li>
    </ul>
    <input v-model="myText" name="deskripsi"/> 
    <button @click="tambah">Add</button>
  </div>
</template>

<script>
import axios from 'axios'
export default { 
  data: function(){
    return {
      todos: [
      ],
      myText : ''
      // nilai: 0,
      // jk: 'lk'
    }
  },
  created : function(){
    axios.get('http://localhost:3000/todo')
    .then(result =>{
      this.todos = result.data
    })
  },
  methods: {
    tambah: function(){
      const newItem = {deskripsi:this.myText}
      axios.post('http://localhost:3000/todo',newItem)
      this.todos.push(newItem)
      this.myText=""
    },
    hapus: function(id){
      axios.delete(`http://localhost:3000/todo/${id}`)
      location.reload()
    }
    
  }
}
</script>

