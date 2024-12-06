<template>
  <div id="app">
    <h1>tarefas</h1>
    <TasksProgess :progress="progress"/>
    <NewTask @taskAdded="addTask"/>
    <TaskGrid :tasks="tasks" @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState"
    />
  </div>
</template>


<script>
import TasksProgess from './components/TasksProgess.vue';
import TaskGrid from './components/TaskGrid.vue';
import NewTask from './components/NewTask.vue';
  export default{
    components:{TasksProgess,NewTask,TaskGrid},
    data(){
      return {tasks:[]
      
    }
  },
  computed:{
    progress(){
      const total = this.tasks.length
      const done= this.tasks.filter(t=> !t.pending).length
      return Math.round(done/total *100)||0

    }
  },
  watch:{
    tasks:{
      deep: true,
      handler(){
        localStorage.setItem('tasks',JSON.stringify(this.tasks))
      }

      
    }
  },
  methods:{
    addTask(task){
      const sameName = t=> t.name === task.name
      const reallyNew= this.tasks.filter(sameName).length ==0
      if(reallyNew){
        this.tasks.push({
          name: task.name,
          pending:task.pending || true
        })
      }
      else{alert("evento ja existe")}
    },

    deleteTask(index) {
      if (index >= 0 && index < this.tasks.length) {
        this.tasks.splice(index, 1);
      } else {
        console.error("Índice inválido:", index);
      }
    },

    toggleTaskState(i){
      
      this.tasks[i].pending = !this.tasks[i].pending
    },
   
  },
  created(){
      console.log('oi')
      const json = localStorage.getItem('tasks')
      const array = JSON.parse(json)
      this.tasks = Array.isArray(array) ? array :[]
  }
  

  }
</script>

<style>
body{
  font-family: sans-serif;
  background: linear-gradient(to right, rgb(23, 31, 44), rgb(107, 76, 76));
  color: #fff;
  
}

#app{
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>