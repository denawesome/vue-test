<template>
    <div>
        <div class="btn-group" role="group">
            <button type="button" class="btn btn-success" data-toggle="modal" data-target="#newTodoModal">
                Add New List
            </button>
            <button @click="$emit('remove-all-todos')" type="button" class="btn btn-danger">
                Delete All
            </button>
        </div>
        <div class="modal fade" id="newTodoModal" tabindex="-1" role="dialog" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title">New Todo List</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <form @submit.prevent="onSubmit">
                        <div class="modal-body">
                            <div class="form-group">
                                <label for="title-name" class="col-form-label">Title:</label>
                                <input type="text" class="form-control" id="title-name" v-model="title">
                            </div>
                        </div>
                        <div class="modal-footer">
                            <button type="text" class="btn btn-secondary" data-dismiss="modal">Close</button>
                            <button type="submit" class="btn btn-primary">Add</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import $ from 'jquery'

export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodoList = {
                    id: Date.now(),
                    title: this.title,
                    data: []
                }
                this.$emit('add-todo-list', newTodoList);
                this.title = '';
                $('#newTodoModal').modal('hide');
            }
        }
    }
}
</script>