<template>
    <div class="container">
        <h2 class="title">Todo App</h2>
        <div class="input-task">
            <input type="text" 
                placeholder="Nhập công việc và bấm  enter để thêm"
                :style="{ border: border }"
                v-model="taskName"
                @focus="focusInput"
                @blur="blurInput"
                @keydown.enter="addTask"
            >
        </div>

        <div class="todo-list" v-if="tasks.length > 0">
            <TodoItem  :tasks="tasks" @deleteTask="removeTask"/>
        </div>

        <div class="todo-empty" v-else>
            <p>Chưa có task nào được thêm</p>
        </div>
    </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
    name: 'Todo',

    components: {
        TodoItem,
    },

    data () {
        return {
            border: '',
            taskName: '',
            tasks: [],
        }
    },

    methods: {
        focusInput: function () {
            this.border = '2px solid #43A1E6';
        },

        blurInput: function () {
            this.border = '';
        },

        addTask: function () {
            let task = {
                name: this.taskName,
                status: false,
            }

            this.tasks.push(task);
            console.log(this.tasks);
            this.taskName = '';
        },

        removeTask: function (data) {
            this.tasks = this.tasks.filter((task, index) => {
                return index != data;
            });
        }
    }
}
</script>

<style lang="scss">
    .container {
        background: #fff;
        width: 500px;
        height: 600px;
        margin: 60px auto;
        border-radius: 10px;

        .title {
            color: #58D07A;
            padding-top: 40px;
        }

        .input-task {
            width: 90%;
            margin: 0 auto;

            input {
                width: 100%;
                padding: 10px 0;
                font-size: 16px;
                border-radius: 9px;
                border: 2px solid #cfd0d1;
                outline: none;
                text-indent: 3px;
            }

            input:hover {
                border: 2px solid #43A1E6;
            }
        }

        .todo-list {
            width: 90%;
            height: 69%;
            margin: 0 auto;
            margin-top: 30px;
            overflow-y: scroll;
        }

        .todo-empty {
            color: #F8877B;
            position: relative;

            p {
                position: absolute;
                left: 24%;
                top: 150px;
                font-size: 20px;
            }

        }
    }
</style>>
