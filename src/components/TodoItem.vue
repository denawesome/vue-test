<template>
    <li class="list-group-item d-flex rounded-0 border-top-0 border-right-0 border-left-0">
        <input 
            type="text"
            :readonly="!isEditing"
            :class="{'form-control-plaintext': !isEditing, 'form-control': isEditing}"
            v-on:handleEditing="isEditing = true"
            v-model="todoItem.title"
        >
        <div class="btn-group btn-group-sm ml-auto" role="group">
            <Edit :data="todoItem" v-on:edit-todo-item="isEditing = !isEditing" />
            <Delete :data="todoItem" v-on:delete-todo-item="$emit('delete-todo-item')" />
        </div>
    </li>
</template>

<script>
import Edit from '@/components/actions/Edit'
import Delete from '@/components/actions/Delete'

export default {
    components: {
        Edit, Delete
    },
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