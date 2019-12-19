<template>
	<div class="col">
		<TodosListActions 
			v-on:add-todo-list="addTodoList"
			v-on:remove-all-todos="removeAllTodos"
		/>
		<hr>
		<div class="accordion w-100" id="todosList" v-if="todos.length">
			<div class="card" v-for="(list, index) in todos" :key="list.id">
				<div class="card-header" :id="`heading-${index}`">
					<button 
						class="btn btn-link" 
						type="button"
						data-toggle="collapse" 
						:aria-expanded="index === 0 ? true : false" 
						:data-target="`#collapse-${index}`" 
						:aria-controls="`collapse-${index}`">{{ list.title }}</button>
					<div class="ml-auto actions-wrapper">
						<SingleListActions 
							v-on:remove-todo-list="removeTodoList"
							:todoList="list" />
					</div>
				</div>
				<div class="collapse" data-parent="#todosList"
					:id="`collapse-${index}`"
					:class="{show: index === 0 ? true : false}"
					:aria-labelledby="`heading-${index}`">
					<div class="card-body">
						<TodoList 
							:todoList="list" 
							v-on:remove-todo-from-list="removeTodoFromList"
						/>
					</div>
				</div>
			</div>
		</div>
		<div v-else class="alert alert-secondary" role="alert">
			No Todos 
		</div>
	</div>
</template>

<script>
import TodoList from '@/components/TodoList'
import SingleListActions from '@/components/actions/SingleListActions'
import TodosListActions from '@/components/actions/TodosListActions'

export default {
	components: {
		TodoList, SingleListActions, TodosListActions
	},
	data() {
		return {
			todos: [{ 
				id: 1,
				title: 'January',
				data: [
					{ id: 1, title: 'Make something in January 1', completed: false },
					{ id: 2, title: 'Make something in January 2', completed: false },
					{ id: 3, title: 'Make something in January 3', completed: false },
					{ id: 4, title: 'Make something in January 4', completed: false },
					{ id: 5, title: 'Make something in January 5', completed: false },
				]
			}, { 
				id: 2,
				title: 'February',
				data: [
					{ id: 1, title: 'Make something in February 1', completed: false },
					{ id: 2, title: 'Make something in February 2', completed: false },
					{ id: 3, title: 'Make something in February 3', completed: false },
					{ id: 4, title: 'Make something in February 4', completed: false },
					{ id: 5, title: 'Make something in February 5', completed: false },
				]
			}, { 
				id: 3,
				title: 'March',
				data: [
					{ id: 1, title: 'Make something in March 1', completed: false },
					{ id: 2, title: 'Make something in March 2', completed: false },
					{ id: 3, title: 'Make something in March 3', completed: false },
					{ id: 4, title: 'Make something in March 4', completed: false },
					{ id: 5, title: 'Make something in March 5', completed: false },
				]
			}]
		}
	},
	methods: {
		removeTodoFromList(options) {
			this.todos = this.todos.filter((list) => {
				if ( list.id === options.todoListId ) {
					list.data = list.data.filter(todoItem => todoItem.id !== options.todoItemId);
				}

				return list;
			});
		},
		removeTodoList(id) {
			this.todos = this.todos.filter(list => list.id !== id);
		},
		addTodoList(newTodoList) {
			this.todos.push(newTodoList);
		},
		removeAllTodos() {
			this.todos = [];
		}
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.accordion > .card {
  overflow: visible;
}
.card-header {
  display: flex;
}
.card-body {
  padding: 0;
}
</style>
