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
    <li v-bind:title="todo">
      {{ todo.slice(0, 10) + '...' }}
    </li>
    <hr>
    <li
        v-for="todo in filteredTodoItems"
        v-bind:key="todo.id"
        class="todo-item"
        v-bind:class="{'done': todo.done}"
        v-on:click="todo.done = !todo.done">
      <span v-if="todo.done">✓</span>
      {{ todo.text }}
    </li>
  </ul>
</template>

<script>
import * as _ from "lodash"
export default {
  name: 'ToDoList',
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
