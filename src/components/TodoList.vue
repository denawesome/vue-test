<template>
	<div class="card">		
		<div class="card-header d-inline-flex" :id="`heading-${index}`">
			<button v-if="!editing" :aria-expanded="index === 0 ? true : false" :data-target="`#collapse-${index}`" :aria-controls="`collapse-${index}`" class="btn btn-link" type="button" data-toggle="collapse">
				{{ todoList.title }}
			</button>
			<div v-else>
				<input type="text" class="form-control" v-model="todoList.title">
			</div>
			<div class="btn-group btn-group-sm ml-auto" role="group">
				<Edit :data="todoList" v-on:edit-todo-list="editing = !editing" />
				<Delete :data="todoList" v-on:delete-todo-list="$emit('delete-todo-list', todoList.id)" />
			</div>
		</div>
		<div class="collapse" data-parent="#todosList"
			:id="`collapse-${index}`"
			:class="{show: index === 0 ? true : false}"
			:aria-labelledby="`heading-${index}`">
			<div class="card-body">
				<TodoItem 
					v-for="todoItem in todoList.data" 
					:key="todoItem.id"
					:todoItem="todoItem"
					v-on:delete-todo-item="deleteTodo"
				/>
				<div v-if="!todoList.data.length">
					<div class="alert alert-info" role="alert">
						No Todos
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
import Edit from '@/components/actions/Edit'
import Delete from '@/components/actions/Delete'

export default {
	data() {
		return {
			editing: false
		}
	},
	props: {
		todoList: {
			type: Object,
			required: true
		},
		index: Number
	},
	components: {
		TodoItem, Edit, Delete
	},
	methods: {
		deleteTodo(id) {
			this.$emit('delete-todo-from-list', {
				todoListId: this.todoList.id,
				todoItemId: id
			});
		}
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
ul form:last-child li {
	border-bottom: none;
}
</style>
