<template>
  <div class="todo">
    <input type="checkbox" class="todo-checkbox" />
    <div class="todo-content">
      <div class="todo-content-title">{{ todo.title }}</div>
      <div class="todo-content-description">{{ todo.description }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoComponent",
  props: ["todo"],
  data() {
    return {};
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
    &-title {
      font-size: 16px;
      font-weight: 600;
      color: #333;
      margin-bottom: 2px;
    }
    &-description {
      font-size: 13px;
      font-weight: 400;
      color: #999;
    }
  }
}
</style>
