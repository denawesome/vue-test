<template>
    <button @click="handleEditing" type="button" class="btn btn-primary">
        <i v-if="!editing" class="far fa-edit"></i>
        <i v-else class="far fa-save"></i>
    </button>
</template>

<script>
export default {
    data() {
        return {
            editing: false
        }
    },
    props: {
        data: {
            type: Object,
        }
    },
    methods: {
        handleEditing() {
            this.editing = !this.editing
            this.data.hasOwnProperty('data') ? this.$emit('edit-todo-list', this.data.id) : this.$emit('edit-todo-item', this.data.id);
        }
    }
}
</script>