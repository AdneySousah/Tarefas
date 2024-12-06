<template>
    <div class="New-Task">
        <input 
            v-model="name" 
            @keydown.enter="add" 
            type="text"
            class="form-element input" 
            placeholder="Nova Tarefa?">
       
        <button class="form-element button" @click="add">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', { name: this.name });
            this.name = '';
        }
    }
}
</script>

<style>
.New-Task {
    margin: 35px;
}

.form-element {
    outline: none;
    font-size: 2rem;
    border: 1px solid #fff;
    padding: 5px 10px 8px;
    color: #fff;
}

.input {
    width: 500px;
    background: #fff2;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
}

.button {
    border-left: none;
    background-color: #2196f3;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    color: #fff;
    cursor: pointer;
}
</style>
