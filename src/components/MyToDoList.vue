<template>
  <input v-model="inputValue"><br>
  入力した値: <span style="font-weight: bold;">{{ inputValue }}</span> <br>
  <button v-on:click="handleClick">
    入力内容を追加
  </button>
  <br><br>
  <input
      v-model="filterValue"
      placeholder="フィルタテキスト">
  <ul>
    <MyToDoItem
        v-for="todo in filteredTodoItems"
        v-bind:key="todo.id"
        v-bind:done="todo.done"
        v-on:toggle="todo.done = ! todo.done">
      <b>{{ todo.text }}</b>
    </MyToDoItem>
  </ul>
</template>

<script>
import * as _ from "lodash"
import MyToDoItem from "./MyToDoItem.vue";
export default {
  name: 'MyToDoList',
  components: { MyToDoItem },
  data() {
    const todoItems = [
      { id: 1, done: false, text: 'Go out to sea' },
      { id: 2, text: 'Going to white mountains' }
    ]
    return {
      todo: 'Go out to sea',
      inputValue: '',
      filterValue: '',
      todoItems,
      filteredTodoItems: todoItems
    }
  },
  watch: {
    filterValue() {
      this.updateFilteredTodoItems()
    },
    todoItems: {
      handler() {
        this.updateFilteredTodoItems()
      },
      deep: true
    }
  },
  methods: {
    handleClick() {
      // alert(this.inputValue)
      if (!this.inputValue) {
        alert('値を入力して下さい')
      } else {
        this.todoItems.push({
          id: this.todoItems.length +1,
          text: this.inputValue
        })
        this.inputValue = ''
      }
    },
    updateFilteredTodoItems: _.debounce(function () {
      this.filteredTodoItems =
          this.filterValue
              ? this.todoItems.filter(todo =>
                  todo.text.includes(this.filterValue)
              )
              : this.todoItems
    }, 500)
  },
  // computed: {
  //   filteredTodoItems() {
  //     if (!this.filterValue) {
  //       return this.todoItems
  //     }
  //     return this.todoItems.filter(todo => {
  //       return todo.text.includes(this.filterValue)
  //     })
  //   }
  // }
}
</script>

<style>
.todo-item.done {
  /* 背景を緑色にする */
  background-color: #3fb983;
  color: #ffffff;
} </style>
