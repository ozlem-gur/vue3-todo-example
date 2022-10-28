<template>
  <div class="container">
    <div class="container-title"></div>
    <div class="container-box">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "ContainerComponent",
};
</script>

<style>
.container {
  max-width: 940px;
  margin-right: auto;
  margin-left: auto;
}
</style>
