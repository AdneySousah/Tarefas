<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <TaskItem v-for="(task,i) in tasks" :key="task.name"  @taskDeleted="$emit('taskDeleted',i)" :task="task" @taskStateChanged="$emit('taskStateChanged',i)"></TaskItem>
        </template>
        <p v-else class="no-taslk"> Sua vida está em dia</p>
    </div>
</template>


<script>
import TaskItem from './TaskItem.vue';
export default{
    components:{TaskItem },
    props:{
        tasks:{type: Array, required: true}
    }
}
</script>


<style>
.task-grid{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}
.task-grid .task{
    margin: 10px;
}
.no-task{
    color: #AAA;
    font-size: 1.7rem;
}
</style>