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
                    <div class="buttons">
                        <button @click="modalOpen(index)">編集</button>
                        <button @click="remove(index)">削除</button>
                        <button @click="complete(index)">完了</button>
                    </div>
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
                    <div class="buttons">
                        <button @click="restore(index)">戻す</button>
                    </div>
                </div>
            </ul>
        </div>
        <div class="deleted" v-if="deletedTasks.length !== 0">
            <h3 class="header">削除したタスク</h3>
            <ul>
                <div class="tasklist" v-for="(deletedTask, index) of deletedTasks" :key="deletedTask">
                    <p>{{deletedTask}}</p>
                    <div class="buttons">
                        <button @click="destroy(index)">完全に削除する</button>
                    </div>
                </div>
            </ul>
        </div>
        <div id="update-modal" class="modal">
            <div class="modal-contents">
                <div class="modal-header">
                    <p>編集</p>
                    <span class="modal-close" @click="modalClose()">×</span>
                </div>
                <div class="modal-body">
                    <p>元のタスク：{{tasks[taskNumber]}}</p>
                        <span class="modal-body-text">
                            <input type="text" id="updated-task">
                            <button @click="update()">編集する</button>
                        </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            taskNumber: 0,
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
            const updatedTask = document.getElementById('updated-task').value;
            this.tasks.splice(this.taskNumber, 1, updatedTask);
            this.modalClose();
        },
        modalOpen(index) {
            const updateModal = document.getElementById('update-modal');
            updateModal.style.display = 'block';
            this.taskNumber = index;
        },
        modalClose() {
            const updateModal = document.getElementById('update-modal');
            updateModal.style.display = 'none';
        },
        remove(index) {
            this.deletedTasks.splice(this.deletedTasks.length, 0, this.tasks[index]);
            this.tasks.splice(index, 1);
        },
        restore(index) {
            this.tasks.splice(this.tasks.length, 0, this.completedTasks[index]);
            this.completedTasks.splice(index, 1);
        },
        complete(index) {
            this.completedTasks.splice(this.completedTasks.length, 0, this.tasks[index]);
            this.tasks.splice(index,1);
        },
        destroy(index) {
            this.deletedTasks.splice(index,1);
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

.buttons {
    width: 200px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}

.modal {
    display: none;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    height: 100%;
    width: 100%;
    overflow: auto;
    background-color: rgba(0,0,0,0.5);
}

.modal-contents {
    background-color: #f4f4f4;
    width: 70%;
    margin: 20% auto;
    border-radius: 15px;
}

.modal-header {
    background: rgba(122, 178, 255, 0.3);
    padding: 3px 10px;
    display: flex;
    justify-content: space-between;
}

.modal-body {
    padding: 20px;
}
.modal-body-text {
    display: flex;
    justify-content: space-between;
}

.modal-body input {
    width: 500px;
    padding: 10px 0px;
    font-size: 24px;
}

.modal-close {
    font-size: 2rem;
}

.modal-close:hover {
    cursor: pointer;
}
</style>