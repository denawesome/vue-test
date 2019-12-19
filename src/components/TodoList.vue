<template>
	<ul class="list-group" v-if="todoList.data.length">
		<TodoItem 
			v-for="single in todoList.data" 
			:key="single.id"
			:todoItem="single"
			v-on:remove-todo-item="removeTodo"
		/>
	</ul>
	<ul class="list-group" v-else>
		<li class="list-group-item d-flex rounded-0 border-top-0 border-right-0 border-left-0">No Todos </li>
	</ul>
</template>

<script>
import TodoItem from '@/components/TodoItem'

export default {
	props: {
		todoList: {
			type: Object,
			required: true
		}
	},
	components: {
		TodoItem
	},
	methods: {
		removeTodo(id) {
			this.$emit('remove-todo-from-list', {
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
