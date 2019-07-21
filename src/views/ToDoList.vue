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
    todo_value: "",
    anyThingDoing: false,
    todo_list: [
      {
        title: "THE FIRST THING TO DO",
        doing: false,
        remainTime: 25
      },
      {
        title: "THE SECOND THING TO DO",
        doing: false,
        remainTime: 25
      },
      {
        title: "THE THIRD THING TO DO",
        doing: false,
        remainTime: 25
      }
    ],
    done_list: [{ title: "THE FOURTH THING TO DO" }]
  }),
  methods: {
    addToList: function(value) {
      this.todo_list.push({ title: value });
      this.todo_value = "";
    },
    checkFinished: function(id, isDone) {
      if (isDone) {
        this.done_list.push(this.todo_list[id]);
        this.todo_list.splice(id, 1);
      }
    },
    startToDo: function(index) {
      let listItem = this.todo_list[index];
      console.log(listItem, this.todo_list[index]);
      listItem.doing = true;
      this.$emit("onItemClicked", listItem.title, listItem.remainTime);
    },
    stopToDo: function(index) {
      let listItem = this.todo_list[index];
      listItem.doing = false;
    }
  }
};
</script>

<style scoped>
#icon {
  margin-left: 10px;
}
</style>
