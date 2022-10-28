<template>
  <div class="home">
    <Header :todoCount="toDos.length">{{ toDos.length }} </Header>
    <Container>
      <Todo
        v-for="toDo in toDos"
        :key="toDo.id"
        :todo="toDo"
        @changedTodoEmit="
          (componentData) => changedTodo(componentData, toDo.id)
        "
      ></Todo>
    </Container>
  </div>
</template>

<script>
import Todo from "@/components/Todo.vue";
import Header from "@/components/Header.vue";
import Container from "@/components/Container.vue";

export default {
  components: {
    Todo,
    Header,
    Container,
  },
  data() {
    return {
      toDos: [],
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
