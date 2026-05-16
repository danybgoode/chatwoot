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
    class="bonsai-track group relative h-4 rounded-full w-7 flex-shrink-0 select-none focus:outline-none focus:ring-1 focus:ring-n-brand focus:ring-offset-n-slate-2 focus:ring-offset-2"
    :class="modelValue ? 'bonsai-track-on' : 'bonsai-track-off'"
    role="switch"
    :aria-checked="modelValue"
    @click="updateValue"
  >
    <span class="sr-only">{{ t('SWITCH.TOGGLE') }}</span>
    <span
      class="bonsai-knob-wrapper absolute top-1/2 ltr:left-0.5 rtl:right-0.5 -translate-y-1/2"
      :class="
        modelValue
          ? 'ltr:translate-x-3 rtl:-translate-x-3 group-active:ltr:translate-x-[6px] rtl:group-active:-translate-x-[6px]'
          : 'ltr:translate-x-0 rtl:translate-x-0'
      "
    >
      <span
        class="bonsai-knob block h-3 w-3 rounded-full group-active:w-[18px]"
      />
    </span>
  </button>
</template>

<style scoped>
.bonsai-track {
  transition: all 0.2s ease !important;
}
.bonsai-track-on {
  background: linear-gradient(180deg, #1a5244, #173f35) !important;
}
.bonsai-track-off {
  background: linear-gradient(
      180deg,
      rgba(255, 255, 255, 0.7),
      rgba(255, 255, 255, 0.34)
    ),
    rgba(183, 215, 206, 0.4) !important;
}
.bonsai-knob-wrapper {
  transition: transform 0.2s ease !important;
}
.bonsai-knob {
  background: #ffffff !important;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 2px 6px rgba(34, 49, 37, 0.22) !important;
  transition: width 0.2s ease !important;
}
</style>
