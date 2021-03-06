<template>
<Dropdown
  :modelValue="open"
  transition="slm-select"
  class="slm-select"
  :class="{ open, disabled }"
  @update:modelValue="setOpen"
>
  <div class="slm-select-value">
    <div>{{ sOptions[modelValue] }}</div>
    <Caret />
  </div>
  <template #dropdown>
    <div
      v-for="opt in unselected"
      :key="opt"
      class="slm-select-item"
      @click="select(opt)"
    >
      {{ sOptions[opt] }}
    </div>
  </template>
</Dropdown>
</template>

<script>

export default {
  name: 'slm-select',
  emits: ['update:modelValue'],
  props: {
    modelValue: {
      type: [String, Number],
      default: '',
    },
    options: {
      type: [Object, Array],
      default: () => ({}),
    },
    disabled: Boolean,
  },
  data() {
    return {
      open: false,
    };
  },
  computed: {
    sOptions() {
      if(Array.isArray(this.options)) {
        const obj = {};
        for(const option of this.options) {
          obj[option] = option;
        }
        return obj;
      }
      return this.options;
    },
    unselected() {
      return Object.keys(this.sOptions).filter(opt => opt !== this.modelValue);
    }
  },
  methods: {
    select(option) {
      this.$emit('update:modelValue', option);
      this.open = false;
    },
    setOpen(open) {
      this.open = !this.disabled && open;
    },
  },
};
</script>

<style lang="postcss">
@import '../../assets/css/global.css';

.slm-select-value {
  display: flex;
  justify-content: space-between;
  width: 100%;
  .caret {
    margin-top: 4px;
    border-color: $text-dark3;
  }
}
.slm-select {
  @mixin select;
  &.open {
    border-bottom-left-radius: 0px;
    border-bottom-right-radius: 0px;
  }
  &.disabled {
    cursor: default;
    background-color: #ddd;
    color: $text-med;
    .slm-select-value .caret {
      border-color: $text-med;
    }
  }
}
.dropdown-menu {
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
.slm-select-item {
  @mixin title-regular 14px;
  @mixin flex-center;
  justify-content: flex-start;
  height: 34px;
  padding: 0 16px;
  background-color: #eee;
}
.slm-select-enter-active, .slm-select-leave-active {
  transition: all 250ms;
  transition-timing-function: cubic-bezier(.53,2,.36,.85);
}
.slm-select-enter-from, .slm-select-leave-active {
  opacity: 0;
}
.slm-select-enter-from, .slm-select-leave-to {
  position: absolute;
}
.slm-select-enter-from {
  transform: translateY(-10px);
}
.slm-select-leave-active {
  transform: translateY(10px);
}
</style>
