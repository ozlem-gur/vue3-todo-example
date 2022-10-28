<template>
  <div class="home">
    <Header :todoCount="toDos.length">{{ toDos.length }} </Header>
    <Container>
      <Todo v-for="toDo in toDos" :key="toDo.id" :todo="toDo"></Todo>
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
  created() {
    fetch("http://localhost:3000/todo")
      .then((res) => res.json())
      .then((data) => (this.toDos = data))
      .catch((err) => console.log(err));
  },
};
</script>

<style></style>
