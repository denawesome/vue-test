<template>
    <form>
        <li class="list-group-item d-flex rounded-0 border-top-0 border-right-0 border-left-0">
            <input 
                type="text"
                :readonly="!isEditing"
                :class="{'form-control-plaintext': !isEditing, 'form-control': isEditing}"
                v-model="todoItem.title"
            >
            <div class="btn-group btn-group-sm" role="group" :class="{hide: isEditing}">
                <button @click="isEditing = true" type="button" class="btn btn-primary">
                    <i class="far fa-edit"></i>
                </button>
                <button @click="$emit('remove-todo-item', todoItem.id)" type="button" class="btn btn-danger">
                    <i class="far fa-trash-alt"></i>
                </button>
            </div>
            <div v-if="isEditing" class="btn-group btn-group-sm" role="group">
                <button @click="isEditing = false" type="button" class="btn btn-primary">
                    <i class="far fa-save"></i>
                </button>
            </div>
        </li>
    </form>
</template>

<script>
export default {
    data() {
        return {
            isEditing: false
        }
    },
    props: {
        todoItem: {
            type: Object,
            required: true
        }
    }
}
</script>
<style scoped>
.form-control-plaintext  {
    outline: none;    
}
input {
    margin-right: 20px;
}
.hide {
    display: none;
}
</style>