<template>
  <div class="container">
    <slot />
  </div>
</template>

<script>
export default {
  name: "ContainerComponent",
};
</script>

<style>
.container {
  max-width: 640px;
  margin-right: auto;
  margin-left: auto;
}
</style>
