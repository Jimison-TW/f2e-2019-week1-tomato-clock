<template>
  <div class="center-inline">
    <div>
      <input type="text" />
      <input type="button" value="新增" />
    </div>
    <div>
      <div>
        <h3 class="list-title">Todo List</h3>
        <ul>
          <li
            v-for="(todo, index) in todo_list"
            :key="todo.id"
            class="list-item"
          >
            <input type="checkbox" v-model="todo.doing" />
            <span>{{ todo.title }}</span>
            <icon
              v-show="!todo.doing"
              name="baseline-play_circle_outline-24px"
              :scale="80"
              id="icon"
              @click.native="startToDo(index)"
            />
            <icon
              v-show="todo.doing"
              name="baseline-pause_circle_outline-24px"
              :scale="80"
              id="icon"
              @click.native="stopToDo(index)"
            />
          </li>
        </ul>
      </div>
      <div>
        <h3 class="list-title">Done List</h3>
        <ul>
          <li v-for="done in done_list" :key="done.id" class="list-item">
            <input type="checkbox" checked="true" />
            {{ done.title }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDoList",
  data: () => ({
    doingID: 0,
    todo_list: [
      {
        title: "THE FIRST THING TO DO",
        doing: false,
        remainTime: 1,
        isDone: false
      },
      {
        title: "THE SECOND THING TO DO",
        doing: false,
        remainTime: 25 * 60,
        isDone: false
      },
      {
        title: "THE THIRD THING TO DO",
        doing: false,
        remainTime: 25 * 60,
        isDone: false
      }
    ],
    done_list: [{ title: "THE FOURTH THING TO DO" }]
  }),
  methods: {
    addToList: function(value) {
      this.todo_list.push({
        title: value,
        doing: false,
        remainTime: 25 * 60,
        isDone: false
      });
    },
    checkFinished: function() {
      this.done_list.push(this.todo_list[this.doingID]);
      this.todo_list.splice(this.todo_list[this.doingID], 1);
    },
    startToDo: function(index) {
      let listItem = this.todo_list[index];
      listItem.doing = true;
      this.$emit("onItemClicked", listItem, this.checkFinished);
    },
    stopToDo: function(index) {
      let listItem = this.todo_list[index];
      listItem.doing = false;
      this.$emit("onItemPaused");
    }
  }
};
</script>

<style scoped>
#icon {
  margin-left: 10px;
}
</style>
