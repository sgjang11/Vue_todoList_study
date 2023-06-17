<template >
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="addBtn fas fa-plus"></i>
        </span>
        <todo-modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고
            </h3>
            <span slot="footer" @click="showModal = false">
                할일을 입력하세요
                <i class="closeModalBtn fas fa-times"></i>
            </span>
        </todo-modal>
    </div>
</template>
<script>
import Modal from './common/todoModal.vue'
export default {
    components: {
        'todo-modal': Modal
    },
    data() {
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                const value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo', value);
                this.clearInput();
            } else {
                this.showModal = !this.showModal
            }
            document.querySelector('input').focus();
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
}
</script>
<style scoped>
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
    display: inline-block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: white;
    vertical-align: middle;
}</style>