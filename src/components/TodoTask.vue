<template>
    <div>
        <div class="create">
            <input style="width: 400px; margin-right: 10px;" @keydown.enter="create" type="text" v-model="newTask">
            <button @click="create">タスクを追加</button>
        </div>
        <div class="todo">
            <h3 class="header">Todo</h3>
            <ul>
                <div class="tasklist" v-for="(task, index) of tasks" :key="task">
                    <p>{{task}}</p>
                    <button @click="update">編集</button>
                    <button @click="remove(index)">削除</button>
                    <button @click="complete(index)">完了</button>
                </div>
            </ul>
        </div>
        <div class="completed">
            <div>
                <h3 class="header">完了したタスク</h3>
                <p class="alert" v-if="completedTasks.length === 0">※完了済のタスクはありません</p>
            </div>
            <ul>
                <div class="tasklist" v-for="(completedTask, index) of completedTasks" :key="completedTask">
                    <p>{{completedTask}}</p>
                    <button @click="restore(index)">戻す</button>
                </div>
            </ul>
        </div>
        <div class="deleted" v-if="deletedTasks.length !== 0">
            <h3 class="header">削除したタスク</h3>
            <ul>
                <div class="tasklist" v-for="(deletedTask, index) of deletedTasks" :key="deletedTask">
                    <p>{{deletedTask}}</p>
                    <button @click="destroy(index)">完全に削除する</button>
                </div>
            </ul>
        </div>
        <div class="modal">
            <input type="text" placeholder="元のタスク">
            <button>編集する</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTask: '',
            tasks: [
                'ex）Vue.jsの勉強をする',
                'ex）部屋の片付けをする',
            ],
            completedTasks: [
                'ex）PHPの学習をする',
                'ex）洗濯物をたたむ',
            ],
            deletedTasks: [
                'ex）削除済みのタスク',
            ],
        };
    },
    methods: {
        create() {
            if (this.newTask.length !== 0) {
                this.tasks.push(this.newTask);
                this.newTask = '';
            } else {
                alert('タスクを入力してください');
            }
        },
        update() {

        },
        remove(index) {
            this.deletedTasks.splice(this.deletedTasks.length, 0, this.tasks[index]);
            this.tasks.splice(index, 1);
        },
        restore(index) {
            this.tasks.splice(this.tasks.length, 0, this.completedTasks[index]);
            this.completedTasks.splice(index, 1);
            console.log(index);
            console.log(this.tasks.length);
        },
        complete(index) {
            console.log('足す前のlength');
            console.log(this.completedTasks.length);
            this.completedTasks.splice(this.completedTasks.length, 0, this.tasks[index]);
            this.tasks.splice(index,1);
            console.log('インデックス');
            console.log(index);
            console.log('length');
            console.log(this.completedTasks.length);
        },
        destroy(index) {
            this.deletedTasks.splice(index,1);
            console.log(this.deletedTasks.length);
        }
    }
}
</script>

<style scoped>
p {
    width: 400px;
}

.todo {
    width: 700px;
    padding: 5px;
    margin: 10px 0px;
    background: rgba(122, 178, 255, 0.3);
    border-radius: 20px;
}

.completed {
    width: 700px;
    padding: 5px;
    margin: 10px 0px;
    background: rgba(43, 255, 146, 0.3);
    border-radius: 20px;
}

.deleted {
    width: 700px;
    padding: 5px;
    background: rgba(124, 124, 124, 0.3);
    border-radius: 20px;
}

.header {
    padding-left: 10px;
    margin: auto;
}

.tasklist {
    display: flex;
}

ul {
    list-style: none;
    margin: auto;
}

.alert {
    font-size: 20px;
    color: red;
}
</style>