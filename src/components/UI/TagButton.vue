<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'TagButton',
};
</script>

<style scoped lang="scss">
.btn {
  cursor: pointer;
  background: $Color8;
  border-radius: 50px;
  color: $Color1;
  padding: 6px 12px;
  border: 0;
  outline: none;
  transition: background 0.2s;

  &:hover {
    background: $Color6;
  }

  &.active,
  &.active:hover {
    @extend %gradient;
    color: $Color2;
  }
}
</style>
