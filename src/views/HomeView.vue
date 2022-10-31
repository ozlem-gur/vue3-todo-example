<template>
  <div class="home">
    <Header
      @todoAddShowEmit="isAddTodoComponentShow = true"
      :todoCount="toDos.length"
      >{{ toDos.length }}
    </Header>
    <TodoAdd
      @todoAddTaskEmit="(componentData) => todoAddTask(componentData)"
      @todoAddRemoveEmit="isAddTodoComponentShow = false"
      v-if="isAddTodoComponentShow"
    />
    <Container>
      <Todo
        v-for="(toDo, index) in toDos"
        :key="toDo.id"
        :todo="toDo"
        @changedTodoEmit="
          (componentData) => changedTodo(componentData, toDo.id)
        "
        @todoDeleteEmit="todoDelete(toDo.id, index)"
        @updateContentEmit="
          (componentData) => updateTodo(componentData, toDo.id)
        "
      ></Todo>
    </Container>
  </div>
</template>

<script>
import Todo from "@/components/Todo.vue";
import Header from "@/components/Header.vue";
import Container from "@/components/Container.vue";
import TodoAdd from "@/components/TodoAdd.vue";

export default {
  components: {
    Todo,
    Header,
    Container,
    TodoAdd,
  },
  data() {
    return {
      toDos: [],
      isAddTodoComponentShow: false,
    };
  },
  methods: {
    changedTodo(componentData, id) {
      fetch(`http://localhost:3000/todo/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ checked: componentData }),
      });
    },
    todoDelete(id, index) {
      fetch(`http://localhost:3000/todo/${id}`, {
        method: "DELETE",
      });
      this.toDos.splice(index, 1);
    },
    updateTodo(componentData, id) {
      fetch(`http://localhost:3000/todo/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: componentData.title,
          description: componentData.description,
        }),
      });
    },
    todoAddTask(componentData) {
      const todoData = {
        title: componentData.title,
        description: componentData.description,
        checked: false,
        id: Math.floor(Math.random() * 100000000),
      };
      fetch(`http://localhost:3000/todo`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(todoData),
      });
      this.toDos.push(todoData);
    },
  },
  created() {
    fetch("http://localhost:3000/todo/")
      .then((res) => res.json())
      .then((data) => (this.toDos = data))
      .catch((err) => console.log(err));
  },
};
</script>

<style></style>
