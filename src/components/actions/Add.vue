<template>
    <div class="text-center">
        <button @click="handleAdd" type="button" class="btn btn-outline-success">
            <i class="far fa-plus-square"></i>
        </button>
    </div>
</template>

<script>
export default {
    methods: {
        handleAdd() {
            this.$emit('add-todo-item');
        }
    }
}
</script>
<style scoped>
.btn {
    margin-top: 10px;
}
</style>