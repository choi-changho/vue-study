<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <font-awesome-icon icon="plus" class="addBtn"/>
    </span>
    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <font-awesome-icon icon="circle-xmark" class="closeModalBtn" @click="showModal = false"/>
      </h3>
      <div slot="body">
        아무것도 입력하지 않으셨습니다.
      </div>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue';
export default {
  data: function () {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem !== '') {
        // 상단에서 넘겨준 이벤트를 실행 => 상단 영역에서 매핑된 이벤트 실행과 함께 파라미터 전달
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function () {
      this.newTodoItem = "";
    },
  },
  components: {
    Modal,
  }
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
