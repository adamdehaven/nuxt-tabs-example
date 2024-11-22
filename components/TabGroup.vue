<template>
  <div :class="['tab-group', `tab-group--${orientation}`]">
    <div class="tab-container">
      <div class="tab-headers" role="tablist" :aria-orientation="orientation">
        <template v-for="(child, index) in $slots.default?.()" :key="child.key">
          <component :is="child" header-only :tab-id="generateId(index)" />
        </template>
      </div>
      <div class="tab-panels">
        <template v-for="(child, index) in $slots.default?.()" :key="child.key">
          <component :is="child" content-only :tab-id="generateId(index)" />
        </template>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, provide, useId } from 'vue';

export interface TabContext {
  activeTabId: Ref<string>;
  registerTab: (id: string, isActive: boolean) => void;
  activateTab: (id: string) => void;
}

const props = withDefaults(defineProps<{
  orientation?: 'horizontal' | 'vertical';
}>(), {
  orientation: 'horizontal'
});

const baseId = useId();
const generateId = (index: number) => `${baseId}-${index}`;

const activeTabId = ref<string>('');
const registeredTabs = ref(new Set<string>());

const registerTab = (id: string, isActive: boolean) => {
  if (!registeredTabs.value.has(id)) {
    registeredTabs.value.add(id);
    if (isActive || registeredTabs.value.size === 1) {
      activeTabId.value = id;
    }
  }
};

const activateTab = (id: string) => {
  activeTabId.value = id;
};

provide('tabContext', {
  activeTabId,
  registerTab,
  activateTab
});
</script>

<style scoped>
.tab-group {
  width: 100%;
}

.tab-container {
  display: flex;
  width: 100%;
}

.tab-group--horizontal .tab-container {
  flex-direction: column;
}

.tab-group--horizontal .tab-headers {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  border-bottom: 1px solid #e5e7eb;
  padding-bottom: 1rem;
  margin-bottom: 1rem;
}

.tab-group--horizontal .tab-panels {
  width: 100%;
}

.tab-group--vertical .tab-container {
  flex-direction: row;
  gap: 2rem;
}

.tab-group--vertical .tab-headers {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  border-right: 1px solid #e5e7eb;
  padding-right: 1rem;
  min-width: 150px;
}

.tab-group--vertical .tab-panels {
  flex: 1;
}
</style>