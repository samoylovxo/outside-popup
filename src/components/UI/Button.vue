<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
};
</script>

<style scoped lang="scss">
.btn {
  font-weight: 500;
  font-size: 12px;
  line-height: 16px;
  padding: 12px 24px;
  border: 1px solid $Color2;
  color: $Color2;
  background-color: transparent;
  border-radius: 6px;
  cursor: pointer;
  outline: none;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s;

  &:hover,
  &:focus {
    background-color: $Color2;
    color: $Color1;
  }

  &:disabled {
    background-color: $Color3;
    color: $Color2;
  }
}

/* Средние девайсы («таблетки», >= 768px) */
@media (min-width: 768px) {
  .btn {
    padding: 16px 32px;
    font-size: 16px;
  }
}
</style>
