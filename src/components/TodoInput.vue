<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <!-- <button v-on:click="addTodo">add</button> -->
        <span class="addContainer">
            <i class="fas fa-plus addBtn" v-on:click="addTodo"></i>
        </span>
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고
                <i class="fas fa-times" @click='close()'></i>
            </h3>
            <input slot="body" type="text" v-model="copyData">
            <h5 slot="footer">{{copyData}}</h5>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data: function(){
        return {
            newTodoItem: "",
            showModal: false,
            copyData: ""
        }
    },
    methods: {
        addTodo: function(){
            if(this.newTodoItem !== ""){
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput: function(){
            this.newTodoItem = '';
        },
        close: function(){
            this.showModal = !this.showModal;
        }
    },
    components: {
        Modal:Modal        
    }
}
</script>

<style scoped>
input:focus{
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style: none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width:3rem;
    border-radius: 0 5px 5px 0;
}
.addBton{
    color: white;
    vertical-align: middle;
}
.closeModalBtn{
    color: #42b983;
}
</style>
