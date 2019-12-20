<template>
	<div class="col">
		<div class="row justify-content-space-between">
			<div class="col-4">
				<TodosListActions 
					v-on:add-todo-list="addTodoList"
					v-on:remove-all-todos="removeAllTodos"
				/>
			</div>
			<div class="col-8">
				<div class="form-group row">
					<label for="filterList" class="col-1 col-form-label">Filter: </label>
					<div class="col-11">
						<input type="text" class="form-control" id="filterList" v-model="filteredTodos">
					</div>
				</div>
			</div>
		</div>
		<hr>
		<div class="accordion w-100" id="todosList" v-if="todos.length">
			<TodoList v-for="(todoList, index) in filteredList"
				:key="todoList.id"
				:todoList="todoList"
				:index="index"
				v-on:delete-todo-from-list="deleteTodoFromList"
				v-on:delete-todo-list="deleteTodoList"
			/>
		</div>
		<div v-else>
			<div class="alert alert-info" role="alert">
				No Lists
			</div>
		</div>
	</div>
</template>

<script>
import TodoList from '@/components/TodoList'
import TodosListActions from '@/components/actions/TodosListActions'

export default {
	components: {
		TodoList, TodosListActions
	},
	data() {
		return {
			filteredTodos: '',
			editingListId: -1,
			todos: [{ 
				id: 1,
				title: 'January',
				data: [
					{ id: 1, title: 'Make something in January 1', completed: false },
					{ id: 2, title: 'Make something in January 3', completed: false },
					{ id: 3, title: 'Make something in January 3', completed: false },
				]
			}, { 
				id: 2,
				title: 'February',
				data: [
					{ id: 1, title: 'Make something in February 1', completed: false },
					{ id: 2, title: 'Make something in February 2', completed: false },
					{ id: 3, title: 'Make something in February 3', completed: false },
				]
			}, { 
				id: 3,
				title: 'March',
				data: [
					{ id: 1, title: 'Make something in March 1', completed: false },
					{ id: 2, title: 'Make something in March 2', completed: false },
					{ id: 3, title: 'Make something in March 3', completed: false },
				]
			}]
		}
	},
	methods: {
		deleteTodoFromList(options) {
			console.log(options);
			this.todos = this.todos.filter((list) => {
				if ( list.id === options.todoListId ) {
					list.data = list.data.filter(todoItem => todoItem.id !== options.todoItemId)
				}

				return list
			})
		},
		deleteTodoList(id) {
			this.todos = this.todos.filter(list => list.id !== id)
		},
		editTodoList(id) {
			this.editingListId = this.editingListId === id ? -1 : id;
		},
		addTodoList(newTodoList) {
			this.todos.push(newTodoList)
		},
		removeAllTodos() {
			this.todos = []
		}
	},
	computed: {
		filteredList: function() {
			var _filteredList = this.filteredTodos.toLowerCase();

			return this.todos.filter(function(elem) {
				if (_filteredList === '') {
					return true
				} else {
					let lowerCasedTitle = elem.title.toLowerCase();
					return lowerCasedTitle.indexOf(_filteredList) > -1;
				}
			})
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
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter {
  opacity: 0;
}
</style>
