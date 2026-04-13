<script setup>
import { isVNode, computed } from 'vue';
import Icon from 'next/icon/Icon.vue';
import Policy from 'dashboard/components/policy.vue';
import { useSidebarContext } from './provider';

const props = defineProps({
  label: { type: String, required: true },
  to: { type: [String, Object], required: true },
  icon: { type: [String, Object], default: null },
  active: { type: Boolean, default: false },
  component: { type: Function, default: null },
});

const { resolvePermissions, resolveFeatureFlag } = useSidebarContext();

const shouldRenderComponent = computed(() => {
  return typeof props.component === 'function' || isVNode(props.component);
});
</script>

<!-- eslint-disable-next-line vue/no-root-v-if -->
<template>
  <Policy
    :permissions="resolvePermissions(to)"
    :feature-flag="resolveFeatureFlag(to)"
    as="li"
    class="py-0.5 ltr:pl-2 rtl:pr-2 rtl:mr-3 ltr:ml-3 relative text-n-slate-11 child-item before:bg-n-slate-4 after:bg-transparent after:border-n-slate-4 before:left-0 rtl:before:right-0 min-w-0"
  >
    <component
      :is="to ? 'router-link' : 'div'"
      :to="to"
      :title="label"
      class="ios6-nav-item flex h-8 items-center gap-2 px-2 py-1 rounded-lg group min-w-0"
      :class="{
        active: active,
      }"
    >
      <component
        :is="component"
        v-if="shouldRenderComponent"
        :label
        :icon
        :active
      />
      <template v-else>
        <span v-if="icon" class="size-4 grid place-content-center rounded-full">
          <Icon :icon="icon" class="size-4 inline-block" />
        </span>
        <div class="flex-1 truncate min-w-0 text-sm">{{ label }}</div>
      </template>
    </component>
  </Policy>
</template>

<style scoped>
.ios6-nav-item {
  color: #c8c7cc !important;
  background: transparent !important;
}
.ios6-nav-item:hover {
  background: linear-gradient(to bottom, #5a5a5a, #3a3a3a) !important;
  color: #ffffff !important;
}
.ios6-nav-item.active {
  background: linear-gradient(to bottom, #1e84fd, #0060e0) !important;
  color: #ffffff !important;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.4) !important;
}
</style>
