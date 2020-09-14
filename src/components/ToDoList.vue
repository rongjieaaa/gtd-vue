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
      <div class="todo-item" v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && !item.completed">
          <el-button class="todo-button" size="mini" icon="el-icon-check" circle @click="updateStatus(item, true)"></el-button>
          <el-input class="todo-title" size="small" v-model="item.title" @change="updateItem(item)"></el-input>
          <el-button class="todo-button" size="mini" icon="el-icon-delete" circle @click="removeItem(item)"></el-button>
        </template>
      </div>
    </div>

    <!--已完成的-->
    <div>
      <div>已完成的：</div>
      <div class="todo-item" v-for="item in todo.items" :key="item.uuid">
        <template v-if="!item.deleted && item.completed">
          <el-button class="todo-button" size="mini" icon="el-icon-close" circle @click="updateStatus(item, false)"></el-button>
          <el-input class="todo-title" size="small" v-model="item.title" disabled></el-input>
          <el-button class="todo-button" size="mini" icon="el-icon-delete" circle @click="removeItem(item)"></el-button>
        </template>
      </div>
    </div>

  </div>

</template>

<script>
import axios from "axios";
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
    axios.get("http://localhost:8080/task/all").then(res => {
      this.todo.items = res.data;
    })
  },
  methods: {
    addItem() {
      let item = {
        uuid: UUID.v4().split("-").join(""),
        title: "",
        completed: false,
        deleted: false,
      };
      this.todo.items.push(item)
      this.updateItem(item);
    },
    removeItem(item) {
      item.deleted = true;
      this.updateItem(item);
    },
    updateStatus(item, status) {
      item.completed = status;
      this.updateItem(item);
    },
    updateItem(item) {
      debugger
      window
      axios.post("http://localhost:8080/task/save", item).then(res => {
      })
    }

  }
}
</script>

<style scoped>

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
