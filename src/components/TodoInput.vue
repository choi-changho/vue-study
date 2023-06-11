<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <font-awesome-icon icon="plus" class="addBtn"/>
    </span>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem !== '') {
        // 상단에서 넘겨준 이벤트를 실행 => 상단 영역에서 매핑된 이벤트 실행과 함께 파라미터 전달
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      }
    },
    clearInput: function () {
      this.newTodoItem = "";
    }
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
</style>
