<script setup lang="ts">
import { computed } from 'vue'
import { withBase } from 'vitepress'

const props = defineProps<{
  /** Page, file or external URL the button opens */
  link: string
  /** Render in the more subtle secondary style */
  secondary?: boolean
}>()

const isExternal = computed(() => /^https?:\/\//.test(props.link))
const href = computed(() => (isExternal.value ? props.link : withBase(props.link)))
</script>

<template>
  <a
    class="download-button"
    :class="{ secondary }"
    :href="href"
    :target="isExternal ? '_blank' : undefined"
    :rel="isExternal ? 'noreferrer' : undefined"
  >
    <svg
      class="download-button-icon"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      aria-hidden="true"
    >
      <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" />
      <polyline points="7 10 12 15 17 10" />
      <line x1="12" y1="15" x2="12" y2="3" />
    </svg>
    <slot>Download</slot>
  </a>
</template>

<style scoped>
.download-button {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin: 8px 0;
  padding: 0 20px;
  height: 40px;
  border: 1px solid var(--vp-button-brand-border);
  border-radius: 20px;
  background-color: var(--vp-button-brand-bg);
  color: var(--vp-button-brand-text) !important;
  font-size: 14px;
  font-weight: 600;
  line-height: 38px;
  text-decoration: none !important;
  transition: border-color 0.25s, background-color 0.25s;
}

.download-button:hover {
  border-color: var(--vp-button-brand-hover-border);
  background-color: var(--vp-button-brand-hover-bg);
  color: var(--vp-button-brand-hover-text) !important;
}

.download-button.secondary {
  border-color: var(--vp-c-divider);
  background-color: var(--vp-c-bg-soft);
  color: var(--vp-c-text-1) !important;
}

.download-button.secondary:hover {
  border-color: var(--vp-c-brand-1);
  background-color: var(--vp-c-bg-elv);
}

.download-button-icon {
  width: 16px;
  height: 16px;
  flex-shrink: 0;
}
</style>
