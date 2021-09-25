<template>
  <div :class="['root', { open: isShow }]">
    <Button @click="isShow = !isShow">Налоговый вычет</Button>
    <Popup
      @close="(show) => (this.isShow = show)"
      :show="isShow"
      v-if="isShow"
    />
  </div>
</template>

<script>
import Popup from '@/components/Popup.vue';

export default {
  name: 'App',

  components: {
    Popup,
  },

  data: () => ({
    isShow: false,
  }),
};
</script>

<style lang="scss">
.root {
  position: relative;
  @extend %gradient;
  box-shadow: 0px -0.11px 16.9495px rgba(183, 187, 225, 0.33);
  min-height: 100vh;
}

.open {
  background: $Color2;
}
</style>
