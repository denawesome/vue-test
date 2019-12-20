<template>
    <button @click="handleDelete" type="button" class="btn btn-danger">
        <i class="far fa-trash-alt"></i>
    </button>
</template>

<script>
export default {
    props: {
        data: {
            type: Object,
        }
    },
    methods: {
        handleDelete() {
            this.data.hasOwnProperty('data') ? this.$emit('delete-todo-list', this.data.id) : this.$emit('delete-todo-item', this.data.id);
        }
    }
}
</script>