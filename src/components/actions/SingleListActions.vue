<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-primary"><i class="far fa-edit"></i></button>
        <button @click="$emit('remove-todo-list', todoList.id)" type="button" class="btn btn-danger"><i class="far fa-trash-alt"></i></button>
    </div>
</template>

<script>
export default {
    props: {
        todoList: {
            type: Object,
            required: true
        }
    }
}
</script>