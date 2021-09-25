<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'AddButton',
};
</script>

<style scoped lang="scss">
.btn {
  font-weight: 500;
  font-size: 12px;
  line-height: 16px;
  padding-top: 12px;
  padding-bottom: 12px;
  width: 100%;
  color: $Color2;
  @extend %gradient;
  box-shadow: 0px 0px 24px rgba(234, 0, 41, 0.33);
  border-radius: 6px;
  border: 0;
  cursor: pointer;
  outline: none;
  transition: all 0.3s;
  margin-top: auto;

  &:hover,
  &:focus {
    background-color: $Color4;
  }

  &:disabled {
    background-color: $Color3;
  }
}

@media (min-width: 768px) {
  .btn {
    padding-top: 16px;
    padding-bottom: 16px;
    font-size: 16px;
    line-height: 24px;
  }
}
</style>
