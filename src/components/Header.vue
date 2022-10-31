<template>
  <div class="header">
    <Container class="header-container">
      <div class="header-title">
        Todo
        <span class="header-title-count">
          <slot />
        </span>
      </div>
      <div class="header-icons">
        <span @click="todoAddShow" class="material-icons"> add_circle </span>
      </div>
    </Container>
  </div>
</template>

<script>
import Container from "@/components/Container.vue";
export default {
  name: "HeaderComponent",
  components: {
    Container,
  },
  methods: {
    todoAddShow() {
      this.$emit("todoAddShowEmit");
    },
  },
};
</script>

<style lang="scss">
.header {
  border-bottom: 1px solid rgb(222, 222, 224);
  padding-top: 10px;
  padding-bottom: 10px;
  position: relative;

  &-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &-icons {
    cursor: pointer;
    .material-icons {
      color: #999;
      &:hover {
        color: #333;
      }
    }
  }
  &-title {
    font-size: 22px;
    font-weight: 800;
    display: flex;
    align-items: center;

    &-count {
      font-weight: 400;
      background-color: #f6f5fa;
      padding: 2px 10px;
      font-size: 16px;
      color: #444444;
      border-radius: 12px;
      margin-left: 8px;
    }
  }
}
</style>
