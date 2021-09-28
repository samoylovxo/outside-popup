<template>
  <div class="popup">
    <div class="content">
      <span @click="closePopup" class="close"></span>
      <h1 class="title">{{ title }}</h1>
      <p class="description">
        {{ description }}
      </p>

      <Form
        @showCalculate="(v) => (showSection = v)"
        :showSection="showSection"
      />

      <Calculation v-if="showSection" />

      <div class="choise">
        <h2 class="choise-title">Что уменьшаем?</h2>
        <div @click="pickMode" class="btn-row">
          <Button class="active tag-btn" style="margin-right: 8px"
            >Платеж</Button
          >
          <Button class="tag-btn">Срок</Button>
        </div>
      </div>

      <Button class="second-btn">Добавить</Button>
    </div>
  </div>
</template>

<script>
import Form from './Form.vue';
import Calculation from './Calculation.vue';

export default {
  components: {
    Form,
    Calculation,
  },

  props: {
    show: {
      required: true,
      type: Boolean,
    },
  },

  data: () => ({
    showSection: false,
    title: 'Налоговый вычет',
    description:
      'Используйте налоговый вычет чтобы погасить ипотеку досрочно. Размер налогового вычета составляет не более 13% от своего официального годового дохода.',
  }),

  methods: {
    closePopup() {
      this.$emit('close', !this.show);
    },
    pickMode(e) {
      const { target } = e;
      const row = document.querySelector('.btn-row');

      [...row.children].forEach((btn) => {
        if (btn.classList.contains('active')) {
          btn.classList.remove('active');
        }
      });

      target.classList.add('active');
    },
  },
};
</script>

<style scoped lang="scss">
.popup {
  position: fixed;
  width: 100%;
  height: 100%;
  min-height: 100vh;
  z-index: 999;
  overflow-y: scroll;
}

.content {
  background-color: $Color2;
  min-height: 100%;
  display: flex;
  flex-direction: column;
  padding: 32px 16px;
  position: relative;
}

.close {
  display: block;
  margin-left: auto;
  background-image: url(~@/assets/jam_close.svg);
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  width: 24px;
  height: 24px;
  cursor: pointer;
  position: absolute;
  right: 16px;
  top: 16px;
}

.title {
  font-weight: 500;
  font-size: 18px;
  margin-bottom: 16px;
}

.description {
  color: $Color5;
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  margin-bottom: 24px;
}

.choise {
  margin-top: 24px;
  margin-bottom: 40px;
}

.choise-title {
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 24px;
}

@media (min-width: 768px) {
  .popup {
    background-color: $Color9;
  }

  .close {
    width: 40px;
    height: 40px;
  }

  .title {
    font-size: 28px;
    line-height: 40px;
  }

  .description {
    font-size: 14px;
    line-height: 24px;
    width: 95%;
  }

  .content {
    background-color: $Color2;
    border-radius: 30px;
    top: 120px;
    max-width: 453px;
    width: 100%;
    min-height: 0;
    padding: 32px;
    margin: auto;
  }

  .choise {
    display: flex;
    align-items: center;
  }

  .choise-title {
    margin-right: 32px;
    margin-bottom: 0;
  }
}

@media (min-width: 1200px) {
  .description {
    font-size: 14px;
    line-height: 24px;
  }

  .content {
    max-width: 552px;
  }
}
</style>
