<template>
  <div id="app">
    <TodoHeader/>
    <TodoInput v-on:addTodoItem="addOneItem"/>
    <TodoList
      v-bind:propsData="todoItems"
      v-on:removeItem="removeOneItem"
      v-on:toggleItem="toggleOneItem"/>
    <TodoFooter
      v-on:clearAll="clearAllItems"
    />
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoList from './components/TodoList.vue';
import TodoInput from './components/TodoInput.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data: function () {
    return {
      todoItems: [],
    }
  },
  methods: {
    addOneItem: function (todoItem) {
      const obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function (todoItem, index) {
      // local storage 제거
      localStorage.removeItem(todoItem.item);
      // 현재 인스턴스 todoItems 배열 내 제거
      this.todoItems.splice(index,1);
    },
    toggleOneItem: function (todoItem, index) {
      // Prop 값으로 넘겨준 값을 다시 상단에 올려서 바꾸는 코드는 좋지 않음
      // todoItem.completed = !todoItem.completed;
      this.todoItems[index].completed = !this.todoItems[index].completed;
      // 로컬스토리지 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function () {
      this.todoItems = [];
      localStorage.clear();
    }
  },
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          const obj = JSON.parse(localStorage.getItem(localStorage.key(i)));
          this.todoItems.push(obj);
        }
      }
    }
  },
  components: {TodoFooter, TodoList, TodoInput, TodoHeader}
}
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F6;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
