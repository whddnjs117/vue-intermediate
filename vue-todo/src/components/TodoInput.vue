<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
    <span class="addContainer" @click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <i class="closeModalBtn fa-solid fa-delete-left" style="font-size: 1.5rem;" @click="showModal = false"></i>
      </h3>
      <h3 slot="body">
        아무것도 입력하지 않으셨습니다.
      </h3>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data : function() {
    return {
      newTodoItem : "", 
      showModal : false 
    }
  },
  methods: {
    addTodo : function() {
      if(this.newTodoItem !== '') {
        this.$emit('addTodoItem',this.newTodoItem)
        this.clearInput();
      } else {
        this.showModal = true
      }
    },
    clearInput : function() {
      this.newTodoItem = '';
    }
  },
  components : {
    Modal : Modal
  }
}
</script>

<style scoped>
input:focus {
  outline:none;
}
.inputBox {
  background: white;
  height: 54px;
  line-height: 50px;
  border-radius:5px;
}

.inputBox input {
  border-style:none;
  font-size :0.9rem;
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478F8, #8763FB);
  display:block;
  width:3rem;
  border-radius:0 5px 5px 0;
}

.addBtn {
  color : white;
  vertical-align:middle;
}

.closeModalBtn {
  color :#42b983
}
</style>