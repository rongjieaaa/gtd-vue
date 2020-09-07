<template>

  <div class="todo-content">

    <!--头部-->
    <div class="todo-head">
      {{todo.title}}
    </div>

    <!--增加子项-->
    <div class="todo-addItem">
      <button @click="addItem">增加子项</button>
    </div>

    <!--未完成的-->
    <div class="todo-uncompleted">
      <div class="todo-uncompleted-title">未完成的：</div>
      <div class="todo-uncompleted-item" v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && !item.completed">
          <input type="checkbox" v-model="item.completed" />
          <input v-model="item.title" />
          <button @click="removeItem(item)" >移除</button>
        </template>
      </div>
    </div>

    <!--已完成的-->
    <div class="todo-completed">
      <div class="todo-completed-title">已完成的：</div>
      <div class="todo-completed" v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && item.completed">
          <input type="checkbox" v-model="item.completed" />
          <input v-model="item.title" />
          <button @click="removeItem(item)" >移除</button>
        </template>
      </div>
    </div>

  </div>

</template>

<script>
import UUID from "uuid";
export default {
  data() {
    return {
      todoList: [
        {
          title: "todoList",
          items: [],
          completed: [],
        }
      ],
      todo: undefined,
    }
  },
  created() {
    if(this.todoList && this.todoList.length && !this.todo) {
      this.todo = this.todoList[0];
    }
  },
  methods: {
    addItem() {
      this.todo.items.push({
        uuid: UUID.v4().split("-").join(""),
        completed: false,
        deleted: false,
      })
    },
    removeItem(item) {
      item.deleted = true;
    },
  }
}
</script>

<style scoped>
</style>
