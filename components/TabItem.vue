<template>
  <template v-if="headerOnly">
    <div 
      class="tab-header"
      :class="{ 'tab-header--active': isActive }"
      role="tab"
      :id="`tab-${tabId}`"
      :aria-controls="`panel-${tabId}`"
      :aria-selected="isActive"
      tabindex="0"
      @click="activate"
      @keydown.space.prevent="activate"
      @keydown.enter.prevent="activate"
    >
      <slot name="header"></slot>
    </div>
  </template>
  <template v-else-if="contentOnly">
    <div 
      class="tab-content"
      role="tabpanel"
      :id="`panel-${tabId}`"
      :aria-labelledby="`tab-${tabId}`"
      tabindex="0"
      v-show="isActive"
    >
      <slot></slot>
    </div>
  </template>
</template>

<script setup lang="ts">
import { inject, computed } from 'vue';
import type { TabContext } from './TabGroup.vue';

const props = withDefaults(defineProps<{
  active?: boolean;
  headerOnly?: boolean;
  contentOnly?: boolean;
  tabId: string;
}>(), {
  active: false,
  headerOnly: false,
  contentOnly: false
});

const tabContext = inject('tabContext') as TabContext;
const isActive = computed(() => tabContext.activeTabId.value === props.tabId);

function activate() {
  tabContext.activateTab(props.tabId);
}

if (props.active) {
  tabContext.registerTab(props.tabId, true);
}
</script>

<style scoped>
.tab-header {
  cursor: pointer;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  transition: background-color 0.2s;
  white-space: nowrap;
}

.tab-header:hover {
  background-color: #f3f4f6;
}

.tab-header--active {
  background-color: #e5e7eb;
  font-weight: bold;
}

.tab-content {
  padding: 1rem;
  width: 100%;
}
</style>