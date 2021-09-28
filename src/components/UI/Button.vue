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
  color: $Color2;
  border-radius: 6px;
  cursor: pointer;
  outline: none;
}

.main-btn {
  padding: 12px 24px;
  border: 1px solid $Color2;
  background-color: transparent;
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

.second-btn {
  padding-top: 12px;
  padding-bottom: 12px;
  width: 100%;
  @extend %gradient;
  box-shadow: 0px 0px 24px rgba(234, 0, 41, 0.33);
  border: 0;
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

.tag-btn {
  cursor: pointer;
  background: $Color8;
  border-radius: 50px;
  color: $Color1;
  padding: 6px 12px;
  border: 0;
  outline: none;
  transition: background 0.2s;
  font-size: 14px;
  line-height: 24px;
  font-weight: 400;

  &:hover {
    background: $Color6;
  }

  &.active,
  &.active:hover {
    @extend %gradient;
    color: $Color2;
  }
}

.submit-btn {
  display: block;
  background-color: transparent;
  border: none;
  color: $Color4;
  padding: 0;
  margin-top: 8px;
  font-size: 14px;
  line-height: 24px;

  &:hover {
    color: $Color7;
  }
}

@media (min-width: 768px) {
  .btn {
    font-size: 16px;
    line-height: 24px;
  }

  .main-btn {
    padding: 16px 32px;
  }

  .second-btn {
    padding-top: 16px;
    padding-bottom: 16px;
  }

  .tag-btn,
  .submit-btn {
    font-size: 14px;
    line-height: 24px;
  }
}
</style>
