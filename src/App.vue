<script setup>
	
	// import ToDoAdd    from './components/toDoAdd.vue';
	// import ToDoList   from './components/toDoList.vue';
	// import ToDoFooter from './components/toDoFooter.vue';

	import { onMounted, onUpdated, ref, watch } from 'vue';

    const tasks = ref([
        {
            description: 'To make an app',
            completed: true
        },
        {
            description: 'To study english',
            completed: false
        },
        {
            description: 'Training',
            completed: true
        },
        {
            description: 'Playing soccer',
            completed: false
        }
    ]);

	const newTask = ref('');

    const completedTasks = ref([]);


	onMounted(() => {
		console.log(`the component is now mounted.`)
		// Mover tareas completadas al arreglo completedTasks durante la inicialización
		for (const task of tasks.value) {
			if (task.completed) {
				completedTasks.value.push(task);
			}
		}
	});


	const createTask = () => {
		
		console.log(newTask.value);

		if ( newTask.value.trim() != '' ) {
			tasks.value.push({
				description: newTask.value.trim(),
				completed: false
			});
			newTask.value = '';
		}
		
	}

	const toggleCompleted = (index) => {
		tasks.value[index].completed = !tasks.value[index].completed;
	};

	const seeTaskAllTheTime = () => {
		console.log( newTask.value );
	}


	// Watcher que estará constantemente a la escucha de cambios en el arreglo tasks
	watch (
		
		tasks, (newTasks, oldTasks) => {

			// Recorremos las tareas para encontrar las que están completadas
			for (const task of newTasks) {
				
				if ( task.completed && !completedTasks.value.includes(task) ) {
					// Si la tarea está completada y no está en el arreglo completedTasks, la agregamos
					completedTasks.value.push(task);
				}

			}

		}, { deep: true } // Opción para observar cambios profundos en el arreglo tasks

	);


</script>



<template>

	<!-- <ToDoAdd></ToDoAdd>
	<ToDoList></ToDoList>
	<ToDoFooter></ToDoFooter> -->

	<form @submit.prevent="onSubmit" class="mb-5">

		<div class="mb-3">
			<label for="exampleInputEmail1" class="form-label text-white">New Task</label>
			
			<input
				type="text"
				class="form-control"
				v-model="newTask"
				@keypress="seeTaskAllTheTime">

			<div id="nuevaTarea" class="form-text text-white">Add a new to the list</div>
			<span>{{ newTask }}</span>
		</div>

		<button @click="createTask" class="btn btn-primary">Create task</button>

	</form>

	<!-- <ToDoItem v-for="task in tasks" v-bind.tasks="task"></ToDoItem> -->

	<div class="mb-5">
		<div class="list-group">
			
			<a
				v-for="({completed, description}, index) in tasks"
				:key="index"
				class="list-group-item list-group-item-action"
				:class="completed ? 'list-group-item-success through' : ''">

				<input class="form-check-input me-3" type="checkbox" :checked="completed" @click="toggleCompleted(index)">
				<span> {{ index + 1 }} - {{ description }} </span>
			</a>

		</div>
	</div>

	<div class="mt-5">
		<h2 class="text-success">Completed Tasks</h2>
		<div class="list-group">

			<a
				v-for="({completed, description}, index) in completedTasks"
				:key="index"
				class="list-group-item list-group-item-action"
				:class="completed ? 'list-group-item-success' : ''">

				<input class="form-check-input me-3" type="checkbox" :checked="completed" @click="completed = !completed">
				<span> {{ index + 1 }} - {{ description }} </span>
			</a>

		</div>
	</div>

</template>



<style scoped>

	.through {
		text-decoration: line-through;
	}

</style>