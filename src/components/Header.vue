<template>
  <div class="header">
    <Container>
      <div class="header-title">
        Todo
        <span class="header-title-count">
          <slot />
        </span>
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
};
</script>

<style lang="scss">
.header {
  border-bottom: 1px solid rgb(222, 222, 224);
  padding-top: 10px;
  padding-bottom: 10px;

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
