<template>
  <div class="todo">
    <input
      type="checkbox"
      class="todo-checkbox"
      @change="changedTodo"
      v-model="checked"
    />
    <div
      class="todo-content"
      :class="{ 'todo-content-checked': checked }"
      @click="isEditable = true"
    >
      <template v-if="isEditable">
        <input
          class="todo-content-title-input"
          v-model="title"
          @keyup.enter="updateTodo"
        />
        <input
          class="todo-content-description-input"
          v-model="description"
          @keyup.enter="updateTodo"
        />
      </template>
      <template v-else>
        <div class="todo-content-title">
          {{ title }}
        </div>
        <div class="todo-content-description">{{ description }}</div>
      </template>
    </div>

    <div class="todo-icons">
      <span @click="todoDelete" class="material-icons"> delete </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoComponent",
  props: ["todo"],
  data() {
    return {
      checked: this.todo.checked,
      title: this.todo.title,
      description: this.todo.description,
      isEditable: false,
    };
  },
  methods: {
    changedTodo() {
      this.$emit("changedTodoEmit", this.checked);
    },
    todoDelete() {
      this.$emit("todoDeleteEmit");
    },
    updateTodo() {
      this.$emit("updateContentEmit", {
        title: this.title,
        description: this.description,
      });
      this.isEditable = false;
    },
  },
};
</script>

<style lang="scss">
.todo {
  margin-bottom: 0px;
  display: flex;
  align-items: flex-start;
  padding-top: 15px;
  padding-bottom: 15px;
  border-bottom: 1px solid #eee;

  &-checkbox {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 1px solid #ccc;
    appearance: none;
    margin-right: 16px;

    &:checked {
      position: relative;
      &::before {
        content: "";
        background-color: turquoise;
        width: 12px;
        height: 12px;
        position: absolute;
        top: 3px;
        left: 3px;
        border-radius: 100%;
      }
    }
  }
  &-content {
    width: 100%;
    &-title {
      font-size: 16px;
      font-weight: 600;
      color: #333;
      margin-bottom: 2px;
      &-input {
        font-size: 16px;
        font-weight: 600;
        color: #333;
        margin-bottom: 2px;
      }
    }
    &-description {
      font-size: 13px;
      font-weight: 400;
      color: #999;
      &-input {
        font-size: 13px;
        font-weight: 400;
        color: #999;
      }
    }

    &-title-input,
    &-description-input {
      display: flex;
      width: 100%;
      border: none;
      box-shadow: none !important;
      outline: none !important;
      padding: 0;
      letter-spacing: 0.3px;
    }
  }

  &-content-checked {
    text-decoration: line-through;
  }
  &-icons {
    margin-left: auto;
    cursor: pointer;
    .material-icons {
      font-size: 18px;
      color: #999;
      &:hover {
        color: #333;
      }
    }
  }
}
</style>
