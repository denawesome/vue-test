<template>
    <div>
        <div class="btn-group btn-group-sm" role="group" v-if="!editing">
            <button @click="handleEditing" type="button" class="btn btn-primary">
                <i class="far fa-edit"></i>
            </button>
            <button @click="handleDeleting" type="button" class="btn btn-danger">
                <i class="far fa-trash-alt"></i>
            </button>
        </div>
        <div class="btn-group btn-group-sm" role="group" v-if="editing">
            <button @click="handleEditing" type="button" class="btn btn-primary">
                <i class="far fa-edit"></i>
            </button>
            <button @click="handleDeleting" type="button" class="btn btn-danger">
                <i class="far fa-trash-alt"></i>
            </button>
        </div>
    </div>
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
            required: true
        }
    },
    methods: {
        handleEditing() {
            this.editing = true;
            this.data.hasOwnProperty('data') ? this.$emit('editing-todo-list', this.data.id) : this.$emit('editing-todo-item', this.data.id);
        },
        handleDeleting() {
            this.data.hasOwnProperty('data') ? this.$emit('deleting-todo-list', this.data.id) : this.$emit('deleting-todo-item', this.data.id);
        }
    }
}
</script>