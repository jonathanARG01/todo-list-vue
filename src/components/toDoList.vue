<script setup>
    
    import { ref } from 'vue';
    import ToDoItem from './toDoItem.vue';

    const tasks = ref([
        {
            id: '001',
            description: 'To make an app',
            completed: true
        },
        {
            id: '002',
            description: 'To study english',
            completed: false
        },
        {
            id: '003',
            description: 'Training',
            completed: true
        },
        {
            id: '004',
            description: 'Playing soccer',
            completed: false
        }
    ]);

    const tasksCompleted = [];

</script>



<template>

    <div class="mb-5">

        <div class="list-group">
            <ToDoItem v-for="task in tasks" v-bind.tasks="task"></ToDoItem>        
        </div>
    
        <div class="mt-5">
            <h2 class="text-success">Completed Tasks</h2>
            <div class="list-group">
                <ToDoItem v-for="taskCompleted in tasksCompleted"></ToDoItem>        
            </div>
        </div>

    </div>

</template>