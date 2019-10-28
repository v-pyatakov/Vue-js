<template>
    <div class="wrap">
        <header>
            <h1>TODO</h1>
        </header>
        <ul id="todo-list" class="todo-list">
            <li class="todo-item" v-for="(item, index) in todoArr" :key="index">
                <input class="checkbox" type="checkbox" v-model="item.done" v-on:click="patchData(fetchUrl, item.id, {done:!item.done})">
                <input class="textfield " v-model="item.task" v-on:change="patchData(fetchUrl, item.id, {task:item.task})">
                <button class="delete" v-on:click="deleteTask(item, todoArr)">x</button>
            </li>
        </ul>
        <form id="todo-form" class="todo-form" v-on:submit="addTask" onsubmit="return false">
            <input class="add-input" type="text" placeholder="input task ..." name="newTask" v-model="newItem.task">
            <button class="add-button">add</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "TodoList",
        data:function () {
            return {
                name: 'Todo List',
                todoArr:[],
                newItem:{
                    done:false,
                    task:"",
                    id:0
                },
                fetchUrl:"http://localhost:3000/todo"
            }},
        methods: {
            addTask: function(){
                this.postData(this.fetchUrl, this.newItem)
                    .then(res => this.todoArr.push(res));
                this.newItem={
                    done:false,
                        task:"",
                        id:0
                }
            },
            deleteTask:function(todoItem,arr){
                this.deleteData (this.fetchUrl, todoItem.id)
                    .then(function () {
                        arr.forEach(function(item, i) {
                            if(item.id===todoItem.id){
                                arr.splice(i, 1);
                            }
                        });
                    })
            },

            getData: function (url) {
                return fetch(url)
                    .then(data => data.json())
                    .catch(err => console.log(err));
            },
            postData: function (url, item) {
                return fetch(url,{
                    method: 'POST',
                    headers: {"Content-Type": "application/json;charset=UTF-8"},
                    body: JSON.stringify(item)})
                    .then(res => res.json())
                    .catch(err => console.log(err));
            },
            deleteData: function (url, id) {
                return fetch(url+"/"+id,{
                    method: 'DELETE',
                    headers: {"Content-Type": "application/json;charset=UTF-8"}})
                    .then(res => res.json())
                    .catch(err => console.log(err));
            },
            patchData: function (url, id, value) {
                return fetch(url+"/"+id, {
                    method: 'PATCH',
                    body: JSON.stringify(value),
                    headers: {
                        "Content-type": "application/json; charset=UTF-8"
                    }
                })
                    .then(res => res.json())
                    .catch(err => console.log(err));
            }

        },
        created:function () {
            this.getData(this.fetchUrl)
                .then(res => this.todoArr = res);
            }

    }
</script>

<style scoped>
    .wrap {
        width:500px;
        margin:50px auto;
        box-shadow:rgba(0, 0, 0, 0.14) 0 2px 2px 0,
        rgba(0, 0, 0, 0.2) 0 3px 1px -2px,
        rgba(0, 0, 0, 0.12) 0 1px 5px 0;
        border-radius:10px;
    }
    header {
        border-radius:10px 10px 0 0;
        justify-content:center;
        background-image: linear-gradient(to right, #ce9dd3, #b8adea, #9ebdf8, #86cbfb, #79d8f6, #6ddff1, #6ae4e7, #71e9da, #69eccd, #6aedbc, #74eea8, #83ee91);
        color:white;
    }
    h1{
        text-shadow:1px 1px 1px  rgba(0,0,0,.5),
        -1px -1px 1px  rgba(0,0,0,.2);
    }
    header, .todo-item, .todo-form {
        width:100%;
        height:70px;
        display:flex;
        align-items:center;
        padding:0 15px;
    }
    .todo-item{
        border-bottom:1px solid #E0E0E0;
    }
    .checkbox, .textfield, .edit, .delete, .add-input, .add-button {
        margin:0 10px;
        color:#546E7A;
        font-size:11pt;
    }
    .task-done{
        text-decoration: line-through;
    }
    .edit, .delete, .add-button {
        text-transform:capitalize;
    }
    .textfield {
        padding: 5px 0;
    }
    .edit, .delete, .add-button {
        padding:5px 10px;
        border:1px solid #546E7A;
        border-radius:5px;
    }
    .edit:hover, .delete:hover, .add-button:hover {
        background-color: #CFD8DC;
    }
    .textfield{
        flex-grow:1;
    }
    .textfield:focus{
        border-bottom:1px solid #546E7A;
    }
    .todo-form {
        border-radius:0 0 10px 10px;
    }
    .add-input{
        flex-grow:1;
        box-shadow:inset 0 0 3px rgba(0,0,0,0.6);
        padding:5px 10px;
        border-radius:5px;
    }
</style>