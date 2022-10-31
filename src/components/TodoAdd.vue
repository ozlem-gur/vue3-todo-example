<template>
  <Container class="todo-add-container">
    <div class="todo-add">
      <input
        v-model="title"
        class="todo-add-title-input"
        type="text"
        placeholder="Task name here..."
      />
      <input
        v-model="description"
        class="todo-add-description-input"
        type="text"
        placeholder="Description"
      />
    </div>
    <div class="todo-add-buttons">
      <button @click="todoAddRemove" class="todo-add-buttons-cancel">
        Cancel
      </button>
      <button @click="todoAddTask" class="todo-add-buttons-addtask">
        Add Task
      </button>
    </div>
  </Container>
</template>

<script>
import Container from "@/components/Container.vue";
export default {
  name: "TodoAddComponent",
  data() {
    return {
      title: this.title,
      description: this.description,
    };
  },
  components: {
    Container,
  },
  methods: {
    todoAddRemove() {
      this.$emit("todoAddRemoveEmit");
    },
    todoAddTask() {
      this.$emit("todoAddTaskEmit", {
        title: this.title,
        description: this.description,
      });
      this.title = "";
      this.description = "";
    },
  },
};
</script>

<style lang="scss">
.todo-add {
  display: flex;
  flex-direction: column;
  margin-top: 30px;

  &-title-input {
    font-size: 16px;
    font-weight: 600;
    padding: 2px 0;
    margin-bottom: 5px;
    border: none;
    box-shadow: none !important;
    outline: none !important;
    &::placeholder {
      color: #9999;
      opacity: 0.9;
    }
  }

  &-description-input {
    font-size: 13px;
    font-weight: 400;
    padding: 10px 0;
    border: none;
    box-shadow: none !important;
    outline: none !important;
    &::placeholder {
      color: #9999;
      opacity: 0.9;
    }
  }
}
.todo-add-buttons {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
  margin-bottom: 50px;

  &-cancel {
    font-size: 14px;
    padding: 7px 15px;
    border: 1px solid rgba(black, 0.2);
    border-radius: 9px;
    color: #777;
    background-color: transparent;
    margin-right: 13px;
    cursor: pointer;
  }

  &-addtask {
    font-size: 14px;
    border: 1px solid rgba(black, 0.2);
    border-radius: 9px;
    color: white;
    background-color: #672ee3;
    padding: 7px 15px;
    cursor: pointer;
  }
}
</style>
