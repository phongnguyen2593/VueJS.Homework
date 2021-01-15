<template>
    <div>
        <div class="todo-item" v-for="(task,index) in tasks" :key="index">
            <div class="checkbox">
                <input type="checkbox" @click="task.status = !task.status" :checked="task.status">
            </div>
            <div class="task-name" :class="{ taskDone: task.status}">
                {{ task.name }}
            </div>
            <div class="btn-delete" v-show="task.status">
                <input type="button" value="Xóa" @click="deleteTask(index)">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['tasks'],

    methods: {
        deleteTask: function (index) {
            this.$emit('deleteTask', index);
        }
    }
    
}
</script>

<style lang="scss" scoped>
    .todo-item {
        display: flex;
        width: 97%;
        border-bottom: 1px solid #EEF2F6;
        margin-left: 10px;
        line-height: 50px;
        height: 50px;
        .checkbox {
            margin-top: 1px;
            width: 10%;
        }

        .task-name {
            width: 75%;
            text-align: left;
        }
        .btn-delete {
            font-weight: bold;
            color: #fff;
            width: 10%;

            input {
                background-color: #F54B5E;
                border-radius: 3px;
                border: unset;
                font-weight: bold;
                color: #fff;
                cursor: pointer;
                outline: none;
                height: 30px;
                padding: 10px 15px;
                line-height: 100%;
            }
        }

        .taskDone {
            text-decoration: line-through;
        }
    }
</style>
