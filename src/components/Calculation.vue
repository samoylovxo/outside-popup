<template>
  <div class="calculation">
    <h2 class="title">Итого можете внести в качестве досрочных:</h2>
    <div class="row">
      <ul class="list">
        <li class="item" v-for="item in items" :key="item.id">
          <input checked class="checkbox" type="checkbox" :id="item.id" />
          <label class="label" :for="item.id"
            >{{ item.sumPerYear }} рублей
            <span
              >{{ item.id === 2 ? 'во' : 'в' }} {{ item.id }}-{{
                getEndingsNumbers(item.id)
              }}
              год</span
            ></label
          >
        </li>
        <li v-if="remaining" class="item">
          <input class="checkbox" type="checkbox" id="remaining" />
          <label class="label" for="remaining"
            >{{ remaining }} рублей
            <span
              >в {{ items.length + 1 }}-{{
                getEndingsNumbers(items.length + 1)
              }}
              год</span
            ></label
          >
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculation',

  data: () => ({
    items: [],
    sumPerYear: null,
    valueFullYear: null,
    remaining: null,
    maxSum: 260000,
  }),

  methods: {
    calculate(value) {
      this.sumPerYear = value * 12 * 0.13;
      this.valueFullYear = Math.floor(this.maxSum / this.sumPerYear);
      this.remaining = new Intl.NumberFormat('ru-RU').format(
        this.maxSum - this.valueFullYear * this.sumPerYear
      );

      for (let i = 0; i < this.valueFullYear; i++) {
        this.items.push({
          id: i + 1,
          sumPerYear: new Intl.NumberFormat('ru-RU').format(this.sumPerYear),
        });
      }
    },

    getEndingsNumbers(number) {
      if (number === 60 || number === 70 || number === 80) return 'ый';

      if (number === 40) return 'ой';

      const numberPointDecimal = (number / 10).toString();
      const decimal = +numberPointDecimal.substring(
        numberPointDecimal.indexOf('.') + 1,
        numberPointDecimal.length
      );
      const ojDecimal = [2, 6, 7, 8];
      const yjDecimal = [1, 3, 4, 5, 9, 10];

      if (number % 10 === 3 && number !== 13) return 'ий';

      if (yjDecimal.includes(decimal) || (number >= 10 && number <= 21))
        return 'ый';

      if (ojDecimal.includes(decimal)) return 'ой';
    },
  },

  mounted() {
    const input = document.querySelector('.input');
    const formatInput = input.value
      .slice(0, input.value.length - 1)
      .split(' ')
      .join('');

    this.calculate(formatInput);
  },
};
</script>

<style scoped lang="scss">
.calculation {
  margin-top: 16px;
}

.title {
  font-size: 14px;
  font-weight: 500;
  width: 56%;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.item {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding-top: 16px;
  padding-bottom: 16px;
  border-bottom: 1px solid $Color6;
}

.checkbox {
  position: relative;
  width: 1px;
  height: 1px;
  clip: rect(1px, 1px, 1px, 1px);
  cursor: pointer;

  &::before {
    content: '';
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 20px;
    height: 20px;
    background-image: url('~@/assets/unchecked.svg');
    background-size: 20px;
    margin-left: 5px;
  }

  &:not(:checked):hover::before {
    background-image: url('~@/assets/checkbox_hover.svg');
  }

  &:checked::before {
    background-image: url('~@/assets/checked.svg');
  }

  &:disabled::before {
    background-image: url('~@/assets/checkbox_disabled.svg');
  }
}

.label {
  margin-left: 22px;
  cursor: pointer;

  span {
    color: $Color5;
  }
}

@media (min-width: 768px) {
  .title {
    width: 100%;
  }
}
</style>
