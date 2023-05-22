<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고! 
                <i class="closeModalBtn fa-regular fa-xmark" @click="showModal = false"></i>
            </h3>
            <div slot="body">아무것도 입력하지 않았습니다</div>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {

    components: {
        modal: Modal
    },

    data: function() {
        return {
            newTodoItem: "",
            showModal: false
        }
    },

    methods: {
        addTodo: function() {
            if(this.newTodoItem !== '') {
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            }else {
                this.showModal = !this.showModal;
            }
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    },
};
</script>

<style lang="scss" scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #42b983;

}
</style>