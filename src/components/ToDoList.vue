<template>

  <div>

    <!--头部-->
    <div class="todo-head">
      {{todo.title}}
      <el-button class="todo-button" size="mini" icon="el-icon-plus" circle @click="addItem"></el-button>
    </div>

    <!--未完成的-->
    <div>
      <div>未完成的：</div>
      <div v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && !item.completed">
          <el-button class="todo-button" size="mini" icon="el-icon-check" circle @click="item.completed = true;"></el-button>
          <el-input class="todo-title" size="small" v-model="item.title"></el-input>
          <el-button class="todo-button" size="mini" icon="el-icon-delete" circle @click="removeItem(item)"></el-button>
        </template>
      </div>
    </div>

    <!--已完成的-->
    <div>
      <div>已完成的：</div>
      <div v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && item.completed">
          <el-button class="todo-button" size="mini" icon="el-icon-close" circle @click="item.completed = false;"></el-button>
          <el-input class="todo-title" size="small" v-model="item.title"></el-input>
          <el-button class="todo-button" size="mini" icon="el-icon-delete" circle @click="removeItem(item)"></el-button>
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

<style>

.todo-title {
  border: 0px;
  width: 200px;
  margin-left: 5px;
  margin-right: 5px;
}

.todo-button {
  border: 0px;
  margin-left: 5px;
  margin-right: 5px;
}

</style>
