<script setup>
import { useI18n } from 'vue-i18n';

const emit = defineEmits(['change']);

const { t } = useI18n();

const modelValue = defineModel({
  type: Boolean,
  default: false,
});

const updateValue = () => {
  modelValue.value = !modelValue.value;
  emit('change', !modelValue.value);
};
</script>

<template>
  <button
    type="button"
    class="ios6-track group relative h-4 rounded-full w-7 flex-shrink-0 select-none focus:outline-none focus:ring-1 focus:ring-n-brand focus:ring-offset-n-slate-2 focus:ring-offset-2"
    :class="modelValue ? 'ios6-track-on' : 'ios6-track-off'"
    role="switch"
    :aria-checked="modelValue"
    @click="updateValue"
  >
    <span class="sr-only">{{ t('SWITCH.TOGGLE') }}</span>
    <span
      class="ios6-knob-wrapper absolute top-1/2 ltr:left-0.5 rtl:right-0.5 -translate-y-1/2"
      :class="
        modelValue
          ? 'ltr:translate-x-3 rtl:-translate-x-3 group-active:ltr:translate-x-[6px] rtl:group-active:-translate-x-[6px]'
          : 'ltr:translate-x-0 rtl:translate-x-0'
      "
    >
      <span
        class="ios6-knob block h-3 w-3 rounded-full group-active:w-[18px]"
      />
    </span>
  </button>
</template>

<style scoped>
.ios6-track {
  transition: all 0.2s ease !important;
}
.ios6-track-on {
  background: linear-gradient(to bottom, #4cd964, #34b84a) !important;
}
.ios6-track-off {
  background: linear-gradient(to bottom, #d0d0d0, #b8b8b8) !important;
}
.ios6-knob-wrapper {
  transition: transform 0.2s ease !important;
}
.ios6-knob {
  background: #ffffff !important;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 2px 4px rgba(0, 0, 0, 0.4) !important;
  transition: width 0.2s ease !important;
}
</style>
