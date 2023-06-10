<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
        <span class="checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)">
          <font-awesome-icon icon="check"/>
        </span>
        <span v-bind:class="{textCompleted: todoItem.completed}">
          {{ todoItem.item }}
        </span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem.item, index)">
          <font-awesome-icon icon="trash-can" />
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      todoItems: [],
    }
  },
  methods: {
    removeTodo: function (todoItem, index) {
      // local storage 제거
      localStorage.removeItem(todoItem);
      // 현재 인스턴스 todoItems 배열 내 제거
      this.todoItems.splice(index,1);
    },
    toggleComplete: function (todoItem) {
      todoItem.completed = !todoItem.completed;
      // 로컬스토리지 데이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  },
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          var obj = JSON.parse(localStorage.getItem(localStorage.key(i)));
          this.todoItems.push(obj);
        }
      }
    }
  },
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #63acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>
