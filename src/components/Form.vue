<template>
  <form @submit.prevent="validate" class="form">
    <label class="label" for="salary">Ваша зарплата в месяц</label>
    <input
      v-model="inputValue"
      :class="['input', { invalid: inputInvalid }]"
      type="text"
      id="salary"
      placeholder="Введите данные"
    />
    <span v-if="inputInvalid" class="err">Поле обязательно для заполнения</span>
    <Button class="submit-btn" type="submit">Рассчитать</Button>
  </form>
</template>

<script>
import Inputmask from 'inputmask';

export default {
  name: 'Form',

  props: {
    showSection: {
      required: true,
      type: Boolean,
    },
  },

  data: () => ({
    inputValue: '',
    inputInvalid: false,
    show: true,
  }),

  methods: {
    validate() {
      if (this.inputValue.trim() === '') {
        this.inputInvalid = true;
        return;
      }

      this.$emit('showCalculate', !this.showSection);
    },
  },

  watch: {
    inputValue() {
      if (this.inputValue.trim() !== '') this.inputInvalid = false;
    },
  },

  mounted() {
    const im = new Inputmask('99 999 ₽');
    const input = document.querySelector('.input');

    im.mask(input);
  },
};
</script>

<style scoped lang="scss">
.label {
  display: block;
  font-weight: 500;
  margin-bottom: 8px;
}

.input {
  border: 1px solid;
  border-color: $Color6;
  border-radius: 3px;
  outline: none;
  padding: 8px 10px;
  width: 100%;
  transition: all 0.3s;
  color: $Color1;
  font-size: 14px;
  line-height: 24px;

  &:hover {
    border-color: $Color1;
  }

  &::placeholder {
    color: $Color3;
  }

  &:disabled {
    border-color: $Color5;
    color: $Color5;
  }

  &.invalid {
    border-color: $Color4;
  }
}

.err {
  color: $Color4;
  font-size: 10px;
  line-height: 12px;
}
</style>
